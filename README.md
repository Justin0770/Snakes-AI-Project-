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
   
**4.** cd into jetson-inference/python/training/classification. Place the data and model folders here, or add the files within them into existing data and model directories inside the classification directory. Make sure that the file resnet18.onnx is included within the models folder.

   In VSCode, you should have something similar to the image below (the cat_dog model is from an unrelated project):
 
![image](https://github.com/Justin0770/Snakes-AI-Project-/assets/136377327/7672f2fd-958b-4e13-ab1a-eefc30eeec75)

**5.** Run the model inside the jetson-inference/python/training/classification directory using the following command:

*imagenet.py --model=models/snakes/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=data/labels.txt data/test/(Venomous or Nonvenomous)/(INPUT).jpg data/test-results/(OUTPUT).jpg*

Replace (INPUT) with a chosen file from inside the test folder and replace (OUTPUT) with what you would like the resulting output file to be called. If your directories are organized differently than mine, you may want to make alterations to the command to match what you have.


**6.** Check inside the test-results directory, where you should find the result of the model. An example is shown below:

![image](https://github.com/Justin0770/Snakes-AI-Project-/assets/136377327/2f0087f2-2f04-4f5a-a640-b679e7b11d49)

** **

[View a video example here]
