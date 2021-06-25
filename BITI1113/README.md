# Music Recommendation System

## A. PROJECT SUMMARY

**Project Title:** Music Recommendation System

In this project, we will show you how a music recommendation system works. Music recommender system is one of the most used machine learning algorithms in recommendation systems. A recommender (or recommendation) system (or engine) is a filtering system which aim to predict a rating or preference a user would give to an item, eg. a film title, a product, a song, etc.

There are two main types of recommender systems we have used in our project: 

**1) Content-based recommender**

**2)Popularity based recommender**

**Content-based recommender**

This type of receommender system is user-specific classification problem. This classifier learns the user's likes and dislikes from the features of the song.

The most straightforward approach is **keyword matching**.

In a few words, the idea behind is to extract meaningful keywords present in a song description a user likes, search for the keywords in other song descriptions to estimate similarities among them, and based on that, recommend those songs to the user.

How is this performed?

In our project, since we are working with text and words, Term Frequency-Inverse Document Frequency (TF-IDF) can be used for this matching process.

**Team Members:** 
- Thivya Tamil Selvam
- Anbu Selvi A/P M Paramasivan
- Noah Brynner
- Redwan 


- [ ] **Objectives:**
- Break out the project goal into more specific objectives
- [insert]
- [insert]
- [insert]


##  B. ABSTRACT 

In late December 2019, a previous unidentified coronavirus, currently named as the 2019 novel coronavirus, emerged from Wuhan, China, and resulted in a formidable outbreak in many cities in China and expanded globally, including Thailand, Republic of Korea, Japan, United States, Philippines, Viet Nam, and our country (as of 2/6/2020 at least 25 countries). Covid-19 are Person-to-person transmission may occur through droplet or contact transmission and if there is a lack of stringent infection control or if no proper personal protective equipment available, it may jeopardize the first-line healthcare workers.

The best safety measure that can be taken is enforcing the people to wear a face mask whenever they are outside to slow down the COVID-19 infection rate. Mask wearing significantly reduced the amounts of various airborne viruses coming from infected patients, measured using the breath-capturing "Gesundheit II machine" developed by Dr. Don Milton, a professor of applied environmental health and a senior author of the study published April 3 in the journal Nature Medicine. In short, masks can help prevent the spread of COVID-19 and that the more people wearing masks, the better.

As for now, you as a Data Scientist or Machine Learning Engineer or Practitioner are going to use AI technology to recognize people whether they are wearing face mask or not in the public or open space.


![Coding]()
Figure 1 shows the AI output of detecting which user is not wearing a face mask or inappropriate face mask.


## C.  DATASET

We’ll review the dataset we use in our music recommendation system.

Million Songs Dataset contains of two files: triplet_file and metadata_file. The triplet_file contains user_id, song_id and listen time. The metadata_file contains song_id, title, release, year and artist_name. Million Songs Dataset is a mixture of song from various website with the rating that users gave after listening to the song.

There are 3 types of recommendation system: content-based, collaborative and popularity but we have only used content-based and popularity in our project.











I’ll then show you how to implement a Python script to train a face mask detector on our dataset using Keras and TensorFlow.

We’ll use this Python script to train a face mask detector and review the results.

Given the trained COVID-19 face mask detector, we’ll proceed to implement two more additional Python scripts used to:

- Detect COVID-19 face masks in images
- Detect face masks in real-time video streams

We’ll wrap up the post by looking at the results of applying our face mask detector.


There is two-phase COVID-19 face mask detector as shown in Figure 2:

![Figure 2]()
Figure 2: Phases and individual steps for building a COVID-19 face mask detector with computer vision and deep learning 

In order to train a custom face mask detector, we need to break our project into two distinct phases, each with its own respective sub-steps (as shown by Figure 1 above):

- Training: Here we’ll focus on loading our face mask detection dataset from disk, training a model (using Keras/TensorFlow) on this dataset, and then serializing the face mask detector to disk

- Deployment: Once the face mask detector is trained, we can then move on to loading the mask detector, performing face detection, and then classifying each face as with_mask or without_mask

We’ll review each of these phases and associated subsets in detail in the remainder of this tutorial, but in the meantime, let’s take a look at the dataset we’ll be using to train our COVID-19 face mask detector.


Our COVID-19 face mask detection dataset as shown in Figure 3:

![Figure 3]()

Figure 3: A face mask detection dataset consists of “with mask” and “without mask” images. 

The dataset we’ll be using here today was created by PyImageSearch reader Prajna Bhandary.

This dataset consists of 1,376 images belonging to two classes:

- with_mask: 690 images
- without_mask: 686 images

Our goal is to train a custom deep learning model to detect whether a person is or is not wearing a mask.

How was our face mask dataset created?
Prajna, like me, has been feeling down and depressed about the state of the world — thousands of people are dying each day, and for many of us, there is very little (if anything) we can do.

To help keep her spirits up, Prajna decided to distract herself by applying computer vision and deep learning to solve a real-world problem:

- Best case scenario — she could use her project to help others
- Worst case scenario — it gave her a much needed mental escape


## D.   PROJECT STRUCTURE

The following directory is our structure of our project:
- $ tree --dirsfirst --filelimit 10
- .
- ├── dataset
- │   ├── with_mask [690 entries]
- │   └── without_mask [686 entries]
- ├── examples
- │   ├── example_01.png
- │   ├── example_02.png
- │   └── example_03.png
- ├── face_detector
- │   ├── deploy.prototxt
- │   └── res10_300x300_ssd_iter_140000.caffemodel
- ├── detect_mask_image.py
- ├── detect_mask_video.py
- ├── mask_detector.model
- ├── plot.png
- └── train_mask_detector.py
- 5 directories, 10 files


The dataset/ directory contains the data described in the “Our COVID-19 face mask detection dataset” section.

Three image examples/ are provided so that you can test the static image face mask detector.

We’ll be reviewing three Python scripts in this tutorial:

- train_mask_detector.py: Accepts our input dataset and fine-tunes MobileNetV2 upon it to create our mask_detector.model. A training history plot.png containing accuracy/loss curves is also produced
- detect_mask_image.py: Performs face mask detection in static images
- detect_mask_video.py: Using your webcam, this script applies face mask detection to every frame in the stream

In the next two sections, we will train our face mask detector.



## E   TRAINING THE COVID-19 FACE MASK DETECTION

We are now ready to train our face mask detector using Keras, TensorFlow, and Deep Learning.

From there, open up a terminal, and execute the following command:

- $ python train_mask_detector.py --dataset dataset
- [INFO] loading images...
- [INFO] compiling model...
- [INFO] training head...
- Train for 34 steps, validate on 276 samples
- Epoch 1/20
- 34/34 [==============================] - 30s 885ms/step - loss: 0.6431 - accuracy: 0.6676 - val_loss: 0.3696 - val_accuracy: 0.8242
- Epoch 2/20
- 34/34 [==============================] - 29s 853ms/step - loss: 0.3507 - accuracy: 0.8567 - val_loss: 0.1964 - val_accuracy: 0.9375
- Epoch 3/20
- 34/34 [==============================] - 27s 800ms/step - loss: 0.2792 - accuracy: 0.8820 - val_loss: 0.1383 - val_accuracy: 0.9531
- Epoch 4/20
- 34/34 [==============================] - 28s 814ms/step - loss: 0.2196 - accuracy: 0.9148 - val_loss: 0.1306 - val_accuracy: 0.9492
- Epoch 5/20
- 34/34 [==============================] - 27s 792ms/step - loss: 0.2006 - accuracy: 0.9213 - val_loss: 0.0863 - val_accuracy: 0.9688
- ...
- Epoch 16/20
- 34/34 [==============================] - 27s 801ms/step - loss: 0.0767 - accuracy: 0.9766 - val_loss: 0.0291 - val_accuracy: 0.9922
- Epoch 17/20
- 34/34 [==============================] - 27s 795ms/step - loss: 0.1042 - accuracy: 0.9616 - val_loss: 0.0243 - val_accuracy: 1.0000
- Epoch 18/20
- 34/34 [==============================] - 27s 796ms/step - loss: 0.0804 - accuracy: 0.9672 - val_loss: 0.0244 - val_accuracy: 0.9961
- Epoch 19/20
- 34/34 [==============================] - 27s 793ms/step - loss: 0.0836 - accuracy: 0.9710 - val_loss: 0.0440 - val_accuracy: 0.9883
- Epoch 20/20
- 34/34 [==============================] - 28s 838ms/step - loss: 0.0717 - accuracy: 0.9710 - val_loss: 0.0270 - val_accuracy: 0.9922
- [INFO] evaluating network...

|      |    precision    | recall| f1-score | support |
|------|-----------------|-------|----------|---------|
|with_mask|0.99|1.00|0.99|138|
|without_mask|1.00|0.99|0.99|138|
|accuracy| | |0.99|276|
|macro avg|0.99|0.99|0.99|276|
|weighted avg|0.99|0.99|0.99|276|


![Figure 4](https://s3.amazonaws.com/stackabuse/media/creating-simple-recommender-system-python-pandas-2.png)

Figure 4: Figure 10: COVID-19 face mask detector training accuracy/loss curves demonstrate high accuracy and little signs of overfitting on the data

As you can see, we are obtaining ~99% accuracy on our test set.

Looking at Figure 4, we can see there are little signs of overfitting, with the validation loss lower than the training loss. 

Given these results, we are hopeful that our model will generalize well to images outside our training and testing set.


## F.  RESULT AND CONCLUSION

Detecting COVID-19 face masks with OpenCV in real-time

You can then launch the mask detector in real-time video streams using the following command:
- $ python detect_mask_video.py
- [INFO] loading face detector model...
- INFO] loading face mask detector model...
- [INFO] starting video stream...

[![Figure5](https://i9.ytimg.com/vi/jIUN4k0gE-Q/mq1.jpg?sqp=CKCh54MG&rs=AOn4CLBi6Ge6x7CWNenhJ7pK-LKRnwJvMA)](https://youtu.be/jIUN4k0gE-Q)

Figure 5: Mask detector in real-time video streams

In Figure 5, you can see that our face mask detector is capable of running in real-time (and is correct in its predictions as well.



## G.   PROJECT PRESENTATION 

In this project, you learned how to create a COVID-19 face mask detector using OpenCV, Keras/TensorFlow, and Deep Learning.

To create our face mask detector, we trained a two-class model of people wearing masks and people not wearing masks.

We fine-tuned MobileNetV2 on our mask/no mask dataset and obtained a classifier that is ~99% accurate.

We then took this face mask classifier and applied it to both images and real-time video streams by:

- Detecting faces in images/video
- Extracting each individual face
- Applying our face mask classifier

Our face mask detector is accurate, and since we used the MobileNetV2 architecture, it’s also computationally efficient, making it easier to deploy the model to embedded systems (Raspberry Pi, Google Coral, Jetosn, Nano, etc.).

[![demo](https://i9.ytimg.com/vi/pA9An19rEVQ/mq3.jpg?sqp=CKCh54MG&rs=AOn4CLAHhKrP9UG9l5h2Y2gJpaV4DDSZUw)](https://youtu.be/pA9An19rEVQ)

