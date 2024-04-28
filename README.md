<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Webcam and Canvas</title>
  <style>
    /* CSS to style the canvas */
    #myCanvas {
      border: 2px solid black;
      width: 640px; /* Example width */
      height: 480px; /* Example height */
    }
  </style>
</head>
<body>
  <div id="canvasContainer"></div>
  
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.0/p5.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.0/addons/p5.dom.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.0/addons/p5.sound.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/ml5/1.1.5/ml5.min.js"></script>
  <script>
    let video;

    function setup() {
      let canvas = createCanvas(640, 480);
      canvas.parent('canvasContainer'); // Place canvas inside div

      video = createCapture(VIDEO); // Access webcam
      video.size(width, height); // Set video size to match canvas
      video.hide(); // Hide the video component
    }

    function draw() {
      background(255); // Clear the canvas
      image(video, 0, 0, width, height); // Draw the webcam view on the canvas
    }

    // Initialize PoseNet
    let poseNet;
    function initPoseNet() {
      poseNet = ml5.poseNet(video, modelLoaded);
      poseNet.on('pose', gotPoses);
    }

    function modelLoaded() {
      console.log('Model Loaded!');
    }

    function gotPoses(poses) {
      console.log(poses);
    }

    // Call initPoseNet function
    initPoseNet();
  </script>
</body>
</html>
