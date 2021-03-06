
# Tutorial: Contour Drawings II (PhotoSketch and p5.js)

🎉Community Contribution by [Matthew Kenney](http://matthewkenney.site/)

![Header](assets/images/tutorials/tutorial_p5_photosketch/header.png)

This post covers how to develop an interface with PhotoSketch and RunwayML. I'll cover the basics of  PhotoSketch, and how to use p5.js to create an interface that pulls in new PhotoSketch images from RunwayML.

### Requirements
- [RunwayML](https://runwayml.com/)
- [p5.js](https://p5js.org/download/)
- [Socket.IO](https://socket.io)
- [Bootstrap](https://getbootstrap.com/) 
- A webcam or built-in camera

### Code
Find the code for this tutorial [here](https://github.com/runwayml/p5js/tree/master/PhotoSketch/PhotoSketch_Websockets).

### PhotoSketch
PhotoSketch is what is known as a Generative Adversarial Network. The goal of Generative Adversarial Networks are to produce synthetic  images that look like images from the training set. That is, if you feed in images of dogs into a GANs, it should produce an unlimited variety of dog-like images. GANs accomplish this by attempting to learn the probability distribution of the training set.

PhotoSketch is a specific type of GAN called a conditional Generative Adversarial Network. Where regular GANs create images from a random noise, conditional GANs can condition that noise on additional input. This input can be any information, including labels, integers, or other images. PhotoSketch conditions this noise on other images. Pairs of images and sketches of those images are fed into the network. The output is a model that translates between images and sketches.

### How to Start the Model
To set up the PhotoSketch model in RunwayML, click on the **Browse Model** button on the upper-left corner of the interface. Scroll to PhotoSketch and select it. This will take you to a page with further information about the model. 

![Select Model](assets/images/tutorials/tutorial_p5_photosketch/selection.png)

From there we can click the **Add to Workspace** button in the upper right hand corner and select **New Workspace**. RunwayML will suggest a name for your workspace. Feel free to change the name or use the one provided and click **Create**. 

![Model Info](assets/images/tutorials/tutorial_p5_photosketch/info.png)

In the workspace, click the **Run Remotely** button, ensuring that the **Remote GPU Enabled** toggle is turned on. Keep in mind that this model will require a GPU to run, and will cost credits. Click **Preview** for the Output Source. We do not need to choose an Input Source, as we'll be sending images straight from our browser! Note that we have also selected **Socket.io** in the **Network** tab on the right pane of the interface. Here we'll find the messaging protocols for Socket.io and RunwayML.


![Add to Workspace](assets/images/tutorials/tutorial_p5_photosketch/interface.png)

### What the Code Does
Well be using [p5.js](https://p5js.org) to communicate to RunwayML. p5.js is a Javascript-based creative coding framework. By bringing the output into the browser and the p5.js ecosystem, it will give us the flexibility to use the output from the model for other creative purposes. In this example we'll use the websockets messaging protocol to connect with RunwayML via [Socket.IO](https://socket.io/).

### How the Code Works
Websockets are a great way to work with any input/output communication between RunwayML and the browser. This script continuously sends over an image from a browser base web camera input. That input is queried on the model and the output is sent back to the browser.

### The Code in Detail (HTML)
In your html, be sure to include the [p5.js library](https://p5js.org/download/), and the [Socket.IO library](https://socket.io/). In this example, I have also included [Bootstrap](https://getbootstrap.com/) (optional) to make the layout a little nicer. In the body of the `index.html` page, we'll add two buttons, a **Stop** and **Start** button that will give us further control in our sketch. We'll also include a paragraph tag with an ID of **status** to keep track of our connection to RunwayML and give visual feedback. Further, we'll include a div tag with an ID for our sketch. This will attach our future sketch to this div, so that its positioned well on the page. Lastly, we'll include a script tag for our sketch.

### The Code in Detail (JavaScript)
The JavaScript code is commented line by line for your reference, there are 4 important parts to pay attention to.  

### Part 1

![Port Address](assets/images/tutorials/tutorial_p5_photosketch/port.png)


The most important step for this sketch is ensuring that the sketch is connecting to RunwayML and able to communicate with it. This communication happens via websockets. Feel free to change the port as necessary, but be sure that the Socket.io server port in RunwayML matches the server port in the sketch. Here, we have set up RunwayML to communicated via port 3000 (image above), and have also specified port 3000 in our sketch. While running your sketch, with the model running, it should say **Connected** below the camera video. If your sketch and model are running, and you don't see the word **Connected**, be sure to check that your ports match.

```js
var socket = io.connect('http://127.0.0.1:3000/');
```


### Part 2
![Input Requirements](assets/images/tutorials/tutorial_p5_photosketch/input.png)

Here we set up a function **sendImage** to send the image from the users webcam to RunwayML via websockets. We should particularly note the `socket.emit` function and the variables it uses. Socket.emit takes two arguments, an input event into RunwayML and the data we would like to send. Here we are sending the a JSON object where the key (**input**) is an image from the webcam. If we look at the RunwayML input specifications (image above) under the **Network** tab and **socket.io**, we can see that RunwayML is expecting the key to be call **input** and is expecting a **base 64 image** for its value.

```js
  // When there is new data coming in, update the log element
  socket.on('data', function(data) {
    if (shouldLoop) {
      sendImage();
    }
  });

  // Get the current frame and send it to RunwayML using the Canvas API
  function sendImage() {
    ctx.drawImage(video, 0, 0, 300, 280);
    // Send to RunwayML the current element in the canvas
    socket.emit('query', {
        input: canvas.toDataURL('image/jpeg'),
    });
  }
```
  
### Part 3

![Output Requirements](assets/images/tutorials/tutorial_p5_photosketch/output.png)

Just like we want to emit data to RunwayML in the previous function, we also want to read data from RunwayML the display that data on the screen. In this case the model returns a base 64 image as a Javascript object. We'll note the output specifications for RunwayML (image above). here the object is returning a JSON object with **image** as the key and a long string representation of an image for the value. We can use that data in the value of the object to construct visual image by calling **createImage** and **drawImage** before creating a p5 image on our canvas.
```js  
....
// When there is a data event, update the log element
  socket.on('data', newDrawing);
});

....

....

function newDrawing(data){
  if(data && data.image) {
    raw.src = data.image;
    raw.onload = function() {
        img = createImage(raw.width, raw.height);
        img.drawingContext.drawImage(raw, 0, 0);
        image(img, 300, 300); 
      }
    }
}
```

### Part 4
Lastly, we'll create a canvas so that we can continue to create interesting ways of interacting with the models output. Here, we'll create a **setup** and **draw** function, inherent to any p5.js sketch. One thing to note is that we've added a parent class to our canvas, so that it is attached to the DOM in the correct position. From here we can continue to build out fun interaction.
```js
function setup(){
    cnv = createCanvas(windowWidth, windowHeight);
    cnv.parent('p5canvas');
    cnv.style('z-index', '-1');
    cnv.position(0, 0);
    background(0);
}

function draw(){
    fill(255, 0, 0);
    textAlign(CENTER);
    textSize(20);
    text("Now I'm a sketch!", 900, 30)
}
```

### Next Steps
This tutorial discussed how to integrate PhotoSketch into a p5.js application. From here we should be able to expand this sketch in really interesting ways! What would it look like to build a comic strip of people as they pass by the camera? How could we extend this to create a photo booth application? Could we turn the image that we capture into a virtual coloring book? We're excited to see how you'll extend this tutorial in new and exciting directions! 

### Addendum
In this tutorial, we connected PhotoSketch and p5.js using the Socket.IO library. With a few quick changes to our codebase, we can use the same code for StyleTransfer, CycleGAN, Pix2Pix, and many other models that return an image. Take a look at the key/value pairs for these models. If we change the keys being emitted via websockets in the **SendImage** and **NewDrawing** function, the codebase will work with many more models in RunwayML. Happy exploring!
