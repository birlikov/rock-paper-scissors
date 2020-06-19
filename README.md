### This project is basicly taken from [this](https://www.coursera.org/learn/browser-based-models-tensorflow/home/welcome) course on tensorflowjs. 

### Description
It captures images of rock/paper/scissors from webcam(you have to press corresponding buttons), then does training on these images and finally predicts one of rock/paper/scissors from your life webcam video stream. The more examples you show the better you get results. 

### Usage
Run main.html using a web server (for example, Web Server for Chrome)

### Files
 * main.html - the main file we run on browser: it loads tfjs, draws buttons/UI and runs js files
 * webcam.js - a helper js file, which let's us use webcam video stream
 * dataset.js - a dataset class, which preprocesses and loads captured images into a dataset
 * scripts.js - handles button functions, builds and trains the model, makes predictions.

### Key insights:

 * With tensorflowjs we can build deeplearing models, train and inference them right in the browser without sending requests to a server, which is cool for mostly speed and privacy reasons.
 
 * Importing tensorflowjs:
 ```<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest"></script>```
 
 * Defining and building the model is almost like in python:
 ```const model = tf.sequential();
        model.add(tf.layers.dense({units: 1, inputShape: [1]}));
        model.compile({loss:'meanSquaredError', 
                       optimizer:'sgd'});
        model.summary();
 ```
 
 * Training and predicting are also intuitively "fit-predict".
 
 * To convert your python-trained model into tfjs model, 
 first save you python-model: ```model.save(saved_model_path)``` 
 then convert it: ```!tensorflowjs_converter --input_format=keras {saved_model_path} ./```
 
 * To use pre-trained models(ex. mobilenet) we just import it:
 ```<script src="https://cdn.jsdelivr.net/npm/@tensorflow-models/mobilenet@1.0.0"> </script> ```
 and use it:
 ```mobilenet.load().then(model => {
        model.classify(img).then(predictions => {
            console.log(predictions);})}
 ```
 And there are a lot of cool pre-trained models: [link](https://github.com/tensorflow/tfjs-models)
 
            