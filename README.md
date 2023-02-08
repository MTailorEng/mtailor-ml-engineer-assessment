# Design and Train an object detector to detect objects

You have to design and implement a Training Pipeline that can train, test and visualize the model using the dataset provided.

## Assignment Protocols

- You will be given 6 hours at max to complete this assessment
- You can only use Python as a programming Language
- Once you start you have to complete this assessment in those 6 hours, it cannot be paused and resumed later
- You cannot take help from any other person
- You can use Google to search for references
- You can not search on google for design-related things, like what should be loss function, or what should be model architecture.
  - But you can use pre-trained backbones from PyTorch
- [NO SUBMISSION WILL BE ACCEPTED WITHOUT THESE VIDEOS] Record videos for the whole duration of the assessment:
  - Make sure you start screen recording before starting the assessment and submit the screen recording link after you are done with the assessment
    - Make sure to add a detailed walk-through of the codebase you have developed in the screen recording
      - Sharing implementation details, giving a full overview of the codebase
      - Explain Design Decisions related to:
        - Model Architecture
        - Loss Function
        - Dataloader
        - etc.
  - Make sure you record yourself while doing the assignment, you can do this either using a laptop camera or you can use a mobile phone to make your video.
  - The two recordings should be easily downloadable and should require no authentication.
  - The candidate will be rejected if there are no videos submitted.

## Task Details
Design a Training Pipeline to train a object detector with following specs or assumptions:
- Implement & Design Model
  - You can use any backbone
    - Either from PyTorch (torhvision) or any resource online
    - But you need to design head your self (head means how you will use features of the back bone and get the desired outputs)
  - Model needs to detect one object in each image
  - Model should output following for each image passed as input:
    - Whether we have an object or not
    - Where is the object?
      - The bounding box output format should be xmin, ymin, xmax, ymax
      - It is not necessary the model is trained to output exactly this format but the visualize function which shows output should output in this format
    - Either the object is a cat or dog?
    - And which specie the object belongs to? There are in total 9 species: 
      - Cat [3 species]:
        - Abyssinian
        - Birman
        - Persian
      - Dog [6 species]
        - american_bulldog
        - american_pit_bull_terrier
        - basset_hound
        - beagle
        - chihuahua
        - pomeranian
- Implement Custom Dataloader
  - This is obvious as dataset is in a unique format any predifined dataloader wont work
  - Follow best practices of writing custom dataloaders
  - Details of the format of the dataset are defined in the Dataset Details section below
  - Add needed pre-processing that you think would help train a better model or would help as we are using pre-trained weights as starting point
  - Add augmentations that you think would help train a better model
- Implement Loss Function
  - Design and implement a loss function that can handle all of the outputs we have
  - You can use pytorch built-in loss functions
  - There are many scenarios which you need to handle, which one can understand from the dataset details and the model design
- Implement Test Function
  - The test function should be able to run the model on the validation set and output the metrics for all the outputs of the model
  - Select the metrics carefully, there are many scenarios which can change the selection of a metric
  - Keep in mind there are multiple outputs, you would need a metric for each output
- Update Resume Training Functionality using the best weights
  - Current script does not have best weights save functionality
  - The code should be able to resume training from exactly same point from where the training was stopped if model weights file is passed
  - Keep in mind you can not resume training from same point by just loading weights of the model
- Implement a visualize function
  - The input of the function should be path of a folder with images and the weight file
    - Also the output folder path to save outputs
  - This function should return a dictionary of dictionaries with following details for each image:
    - {
        "has_object": True,
        "cat_or_dog": "cat",
        "specie": "persian",
        "xmin": 10,
        "ymin": 10,
        "xmax": 10,
        "ymax": 10
    }
  - And in case there is no object it should have 0 for bbox values, "NA" for "cat_or_dog" and "specie", and False for "has_object".
  - Values of the returned dictionary should be like explained above and keys should be image names including the extension ".jpg" or ".jpeg"
  - Should save output image with bounding box drawn on it, with same name input image but place in the output folder 
- Implement Test Cases to Test Different Functions Written
  - Work on this part in the end if you have time
  - If you have limited time write in words, how and what you would have tested if you had time


## Dataset Details
The dataset has in total 1041 images. Each image has a single object which is either a cat or a dog.
- There are multiple species for both cat and dog.
- The number of images falling in each specie is as follows:
  - basset_hound: 93
  - Birman: 93
  - pomeranian: 93
  - american_pit_bull_terrier: 93
  - american_bulldog: 93
  - Abyssinian: 92
  - beagle: 93
  - Persian: 93
  - chihuahua: 93
  - empty: 142
- The dataset has two folders:
  - images
    - Inside images folder we have 986 images in .jpg folder
  - labels
    - Inside labels folder we have 899 .xml files each file with details of image labels
    - For any image that does not have a cat or dog, there is no corresponding xml file

## Deliverable
- Updated Colab Based Jupyter Notebook:
  - With all the required functionality Implemented
  - Which one can train the model without any errors
  - One should achieve same metrics (Almost same metrics) if I run training using this collab notebook
    - Set default values for everything accordingly, during evaluation we will just run the notebook and use the best weights the notebook saves automatically
- Best weights you have trained
  - We will Evaluate you weights against hold-out test we have and compare results
  - We will use visualize function to generate outputs for each image
  - Upload weights in an easily downloadable location like, Dropbox, Google Drive, Github, etc
- Video Explaining your design decisions
  - Model Design which layers and activation functions you used and why
  - Loss function, which loss functions you used and why
  - How you implemented resume functionality, what were the things you thought would be needed to resume training from exact same point


## Evaluation Criteria
 - Design Decisions
 - Completeness: Did you include all features?
 - Correctness: Does the solution (all deliverables) work in sensible, thought-out ways?
 - Maintainability: Is the code written in a clean, maintainable way?
 - Testing: Is the solution adequately tested?
 - Documentation: Is the codebase well-documented and has proper steps to run any of the deliverables?

## Extra Points
- Model Design should handle any input size
  - Model should not be designed in a way that it can only accept a fixed input size.
- Any Updates in the notebook (Bugs/Implementation Mistakes etc)

## How to submit
- Please upload the code for this project to GitHub, and post a link to your repository below [repo link box, on the left of submit button].
  - You can create a new GitHub repository, by either making a fork/clone of the repo shared above or creating a new repo from scratch
  - Add the final Colab/Jupyter notebook to the repository
- Please upload both videos and your final best weights on Google Drive or any other platform, and paste the link to the folder with both videos in the text box just above the submit button.
- Please paste the commit Id of the latest commit of your Github Repo, which should not be later than 6 hours of time when the repo was created.
  - Please note the submission without the commit id will not be considered.
