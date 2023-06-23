# Snakes-AI Project

SnakesAI uses a retrained resnet-18 network to classify snakes based on whether or not they are venomous. The goal of this project is to help people assess whether a snake is dangerous or not and be able to respond accordingly and stay safe.

For example, in the image below it has accurately identified that this king cobra is venomous.

![image](https://github.com/Justin0770/Snakes-AI-Project-/assets/136377327/2b9fc2ed-d961-4992-8e4a-e02f48a8d803)

## The Algorithm

The algorithm for this program was retrained with transfer learning from the Resnet-18 model that comes packaged with the Jetson Inference Library. It was retrained using the following database from kaggle: https://www.kaggle.com/datasets/adityasharma01/snake-dataset-india (please note that the model was trained on a database of Indian snake species only, which means the current model will likely not perform as well on other snake species). 

The labels file defines the categories: "Venomous" and "Nonvenomous." The AI is then fed images of snakes categorized between these two groups inside the train folder and then evaluates its accuracy with the images contained inside the val/validation folder. It iterates on this process until it has been trained to more accurately recognize the difference between venomous and nonvenomous snakes. This creates the model, which is then converted into the ONNX format so it is easier to share it.

The directory in which the project is included, displayed in VSCode:

![image](https://github.com/Justin0770/Snakes-AI-Project-/assets/136377327/3d74febe-4a69-4b39-880b-9352909a1955)

## Running the Project

**1.** Download the data and model folders from this repository.

**2.** SSH into your Jetson using VSCode/Putty/etc.
   
**3.** Make sure the Jetson Inference Library is installed on your Jetson Nano, as it includes the networks (imagenet, resnet-18) required to run this program.
   
**4.** Create a new directory and name it something related to the project. I named my directory "snakesproject", so replace any future instances of "snakesproject" in these instructions with the name you chose for your directory. Place the data and model folders here and sure that the file resnet18.onnx is inside the model folder.

   In VSCode, you should have something similar to the image below:
 
![image](https://github.com/Justin0770/Snakes-AI-Project-/assets/136377327/c2cb5a36-f597-44c7-8438-15eb1a0c3fc5)

**5.** Within snakesproject, set NET=model and DATASET=data inside of the Linux terminal.

**6.** Run the model inside the jetson-inference/python/training/classification directory using the following command:

*imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/(Venomous or Nonvenomous)/(INPUT).jpg $DATASET/test-results/(OUTPUT).jpg*

Replace (INPUT) with a chosen file from inside the test folder and replace (OUTPUT) with what you would like the resulting output file to be called. If your directories are organized differently than mine, you may want to make alterations to the command to match what you have.


**7.** Check inside the test-results directory, where you should find the result of the model. An example is shown below:

![image](https://github.com/Justin0770/Snakes-AI-Project-/assets/136377327/b4107b66-ff90-4c79-90de-58315b377e10)
 
** **

#Video Demonstration

View a video demonstration at the link below
https://youtu.be/Ua-t79bmobo
