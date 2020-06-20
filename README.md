### This project is the final project of [this](https://www.coursera.org/learn/browser-based-models-tensorflow/home/welcome) course on tensorflowjs. 

### Description
It captures images of rock/paper/scissors from webcam(you have to press corresponding buttons), then does training on these images and finally predicts one of rock/paper/scissors from your life webcam video stream. The more examples you show the better you get results. 

### Usage
Run *main.html* using a web server (for example, Web Server for Chrome)

### Files
 * *main.html* - the main file we run on browser: it loads tfjs, draws buttons/UI and runs js files
 * *webcam.js* - a helper js file, which let's us use webcam video stream
 * *dataset.js* - a dataset class, which preprocesses and loads captured images into a dataset
 * *scripts.js* - handles button functions, builds and trains the model, makes predictions.

### Key insights:

 * With tensorflowjs we can build deeplearing models, train and inference them right in the browser without sending requests to a server, which is cool for mostly speed and privacy reasons.
 
 * Importing tensorflowjs is easy as adding one line in your html file:
 
 ```<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest"></script>```
 
 * Defining and building the model is almost like in python:
 ```const model = tf.sequential();
        model.add(tf.layers.dense({units: 1, inputShape: [1]}));
        model.compile({loss:'meanSquaredError', 
                       optimizer:'sgd'});
        model.summary();
 ```
 
 * Training and predicting are also intuitively "fit-predict".
 
 * To convert your python-trained model into tfjs model, assuming you have saved your model trained with python: ```model.save(saved_model_path)```, you just convert it using python tensorflowjs library(this will create *model.json* file and several binary files storing the weights of neural network): 
 
 ```!tensorflowjs_converter --input_format=keras {saved_model_path} ./```
 
 * Use your saved model in js:
 
 ```
    const MODEL_URL = 'http://127.0.0.1:8887//path-to-you-newly-converted-model.json';
    const model = await tf.loadLayersModel(MODEL_URL)
    console.log(model.summary());
    const result = model.predict(input);
 ```
 
 * To use pre-trained models(ex. mobilenet) we just import and use it:
 ```
 <script src="https://cdn.jsdelivr.net/npm/@tensorflow-models/mobilenet@1.0.0"> </script>  
 
 mobilenet.load().then(model => {
        model.classify(img).then(predictions => {
            console.log(predictions);})}
 ```
 * There are a lot of cool pre-trained models: [link](https://github.com/tensorflow/tfjs-models)
