

---
layout: post
title: Articles AlphSistant
description: Résumé d'articles scientifiques sur des problématiques pertinentes pour AlphSistant
image: assets/images/faq/h2g2.png
---


# Talking Heads - https://arxiv.org/pdf/1905.08233.pdf

* WIIA
    * 2D Talking heads with few-shots capabilities
    * Direct (warping-free) synthesis: enables wider set of expressions and movements 
* STRATEGY
    * Meta-learning / pre-training is crucial for the few shot capabilities
    * Landmark position -> face movements 
    * Architecture is composed of three models: 
        * Embedder: takes initial image  + rasterized landmarks and produces an embedding vector
        * Generator: takes the rasterized image for another frame + embedding vector for initial frame and returns a synthetized the image. Trained on maximizing similarity between synth. image and ground truth (image at the other frame)
        * Discriminator: predicts a realism score and a matching score between a face and rasterized landmarks image 
    * Training in an adversarial fashion + episodic K-shots learning 
    * Need to details loss components 
    * Fine-tuning: 
        * Select a few frames and compute corresponding rasterized landmarks 
        * Possible to directly generate sequences by feeding frames and RL to generator but this alters the face composition 
        * Similar process to the meta learning phase but person-specific and person-generic parameters are jointly optimized
* USEFUL IDEAS: 
    * Requires the availability of the face landmarks location for each video 
    * Landmarks are "drawn" on an image before being sent to the models
    * Perceptual similarity loss is used with a VGG19 face model (specifically trained on a face verification task) 
    * Estimation of a projection matrix 
* TECHNICAL DETAILS :
    * Landmarks are rasterized to a three channel image 
    * AdaIN seems to be used to split the generator parameters into the person-generic parameters and person specific parameters (to be confirmed)
    * Architecture based on image-to-image translation (https://arxiv.org/pdf/1603.08155.pdf)
    * Instance normalization instead of batch-normalization 


# Audio-Driven Facial Animation by Joint End-to-End Learning of Poseand Emotion (Nvidia 2017) - https://research.nvidia.com/sites/default/files/publications/karras2017siggraph-paper_0.pdf

* WIIA
    * 3D Facial animation
    * Audio driven animation: mapping from waveform to 3D vertex coordinates
    * Latent code for expression disambiguation 
* STRATEGY
    * Trained with animation data from mocap -> generates animation for a specific model and audio. Can be transferred with a degree of loss to audio from other speakers 
    * Outputs per-frame position of vertices 
    * 3-5 min of high quality footage 
    * End-to-end training + latent representation of emotional state
    
    * NETWORK ARCHI
        * Three sub-networks: formant analysis, articulation, output network 
        * Formant: extracts short term features (intonation, emphasis)
        * Uses formant output + additionnal emotional vector to predict latent deformation representation 
        * Output network: latent reprez to vertex 


* USEFUL IDEAS: 
    * Uses a short window of audio to determine vertex pos in the center
    * After training, window slides over the audio, sollicitating the network independently each time
    * Formant analysis (?) to produce time varying speech features  
    
* TECHNICAL DETAILS :
    * No residual motion (head movement, blinking etc). Focus only on mouth deformations 
    * AUDIO PROCESSING
        * No specific filters or processing. Only normalization to full dynamic range 
        * Autocorrelation to extract a compact audio representation that consists of a linear filter and an excitation signal (use LPC to perform separation)
        * 520ms of audio in 64 frames with 2x overlap 
    * EMOTIONAL STATES 
        * The approach requires additionnal information to infer expression because similar sounds could be produced by very different expressions: this would lead the model to output statistical mean which is undesired 
        * Learned E-dimensionnal vector: initialize a normal random vector (E = 16 or 24) for each training sample => emotion database 
        * Emotional states need to focus on higher-term variations (?)
    * DATASET 
        * 3D scans, 30 fps, commercial devices for acquisition 
        * For each actor: pangrams (sentences designed to cover as many expressions as possible, 1 to 3 per actor) + in-character material
        * A1: 9034 frames (3872 pangrams, 5162 in-character, 1734 validation)
        * A2: 6762 frames (1722 pangrams, 5040 in-character, 887 validation)
    * LOSS FUNCTIONS:   
        * Three specialized losses: position, motion, regularization 
    * TRAINING: 
        * 3h for A1 on TitanX 




# Speech-driven 3D Facial Animation with Implicit Emotional Awareness:A Deep Learning Approach https://openaccess.thecvf.com/content_cvpr_2017_workshops/w41/papers/Pavlovic_Speech-Driven_3D_Facial_CVPR_2017_paper.pdf


* WIIA
    * LSTM approach for real-time facial anim + estimation secondary motions from speech 
    * Use of acoustic features to represent context and emotional intensity of the speech to ouput 3D rot + blend shapes weights 
* STRATEGY
    * Extract 3D deformations from videos 
        * Two steps: 3D face alignment + refinement 
            * RF predicts alignment + 2D position of landmarks 
            * Refinment: fine-tune 3D deformations to minimize reprojection error 
    * Audio: 
        * Mel-scaled spectrogram, MFCCs, chromagram 


* USEFUL IDEAS: 
    * Contextual state and emotions are represented through audio features (MEL etc) 
    * Ravdess dataset: audio / visual corpus with high rez videos of speeches and emotions -> 3D facial deformations tracking 
    * Head rot + weighted blendshapes 
    
* TECHNICAL DETAILS :
    * 3D face params were estimated using RF 
    * 46 blendshapes

# Capture, Learning, and Synthesis of 3D Speaking Styles https://arxiv.org/pdf/1905.03079.pdf


* WIIA  
    * How to obtain better results in audio-driven facial animation using 4D datasets and ENABLE GENERALIZATION  
    * Any speech signal as input and animates adult faces 
    
* STRATEGY
    * To generalize between subjects, both in terms of audio as well as different facial shapes and motion several particularities were implemented: 
        * Use of DeepSpeech
        * Use of Flame: statistical head model that uses linear transformations to describe identity, expression and neck, jaw and eyeball rot  

    * PIPELINE: 
        * Input is subject specific template + raw audio signal 
        * Output: Target 3D mesh 
        * DeepSpeech extracts speech features: log probs of characters (letters) by frame of 0.02s 
        * Convolutionnal encoder compresses the features 
        * Fully connected decoder outputs 5023 * 3 features

* USEFUL IDEAS: 
    * speaker independant modeling remains challenging and mostly unsolved 
    * The decoder weights are initialized with PCA over vertex displacement in the dataset 
    * Losses: position + velocity loss (introduces temporal stability)

* TECHNICAL DETAILS :
    * Audio / Scans dataset is available at http://voca.is.tue.mpg.de/
        * 12 subjects - 480 sequences of 3s ~ 4s
        * Align a common mesh template to the scans
    * Single NVidia Tesla K20 (~ 10 min/epoch)
    * There are details about the VOCASET
    