# webMidi MegaMacro™

## Running Locally

To run on your local machine you will first need to serve some files. The recommended way to do this is to use the node package [http-server](https://www.npmjs.com/package/http-server). 

```
npm install http-server -g
npm install cors -g
```

Then when in the project folder in the terminal run the command below.

```
http-server -p 4200 --cors
```

This serves the files in the folder at [http://localhost:4200](http://localhost:4200/) and adds a header to get around CORS issues.

## Edit Output CC channels

To use the app with your device of choice you will want to edit the output MIDI CC channels. This is easily done inside the index.html between lines 48 & 63. You could manually add each output to the oCC array or use a for loop to add ranges of CC channels in one go. 

```javascript
48	//Array of CC channel values to map Learner to
49	//CHANGE THESE VALUES TO EDIT OUTPUT CC CHANNELS
50	let oCC = [1,5];
51	//for loops to populate array with CC channel values
52	//Channel 25-37
53	for(let i = 25; i <= 37; i++){
54	  oCC.push(i);
55	}
56	//Channel 39-62
57	for(let i = 39; i <= 62; i++){
58	  oCC.push(i);
59	}
60	////Channel 70-91
61	for(let i = 70; i <= 91; i++){
62	  oCC.push(i);
63	}
```

## How To Use The Tool

1.  Select your input MIDI device by pressing "Get Midi Devices" and select your device from the drop down.

2. Do the same for your MIDI output.

3. Once your MIDI input and output devices are selected press "Start Midi Learn" to begin listening for input Midi CC messages. If you accidentally add a Midi CC that you don't want use "Clear Midi Learn" to start the MIDI learn from scratch.

4. Now you have your input MIDI configured select how many output CC's you want to send using the selector. You will only be able to add as many outputs as you have defined within the code.

   *Make sure you have edited the output CC's within the index.html !*

5. You will now see the Learner.js GUI this allows you to create your dataset which will be used to train your machine learning model. 

   Use randomise to find interesting patches on your output device, or manually adjust the sliders to dial in your desired sound. 

   Note: To improve performance output CC's are only sent when an input CC is received. This means to hear the changes to your MIDI output give one of your input controls a wiggle to send the data.

6. When you have found a patch you like you need to assign it to the position of your MIDI input! To do this set your midi to the desired position/value and press record, due to how machine learning works it's best to provide a few examples for the data set so give your MIDI input a wiggle in the position you want it to be assigned and press stop.

   This has now created a dataset of data pairs of inputs and outputs for your model to learn from.

7. Repeat this process of creating input and output pairs as many times as you want across the range of motion of your input. 

   If you forget to change either your input or output between recording use the Clear Prev button to delete your previous recording.

   *To start just create 2 or 3 input and output groups to build intuition on how the model learns*

8. When you have created your dataset press Train, this will train your machine learning model on your dataset to interpolate between your input and output groups, when it has finished it will automatically run.

9. As this is a machine learning approach sometimes the result isn't what you want if you just want to try again use Clear All to start the dataset creation process from scratch.

## Learner.js

Learner.js provides an interface that allows you to easily record in examples of input and output pairings into a dataset that is saved locally in your browser.

You can then train a model to respond with new outputs when you provide new inputs.

All the storage, threading and GUI needs are taken care of for you and all you have to do is pick what you want to control is what!

You can [follow the guide](https://mimicproject.com/guides/learner) on the MIMIC site to learn more about the library

Or you can [look at the API documentation](https://www.doc.gold.ac.uk/~lmcca002/Learner.html).