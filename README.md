# Machine Learning Engineer Nanodegree
## Capstone Project
## udacity-digit-recognizer
Allison Senden  
October 28th, 2019

## I. Definition

### Project Overview
Digit recognition is being studying by those practicing their computer vision and machine learning skills. I specifically chose this project topic because I would like to get into some work at my current job where they are helping to design a model that can handle taking in and interpreting the information on faxes. This would include handwritten text and digits. I think that many companies can benefit by having a model that can take handwritten notes and interpret them into useable information. This would help to alleviate someone manually completing this task which I could imagine would take hours. If the company can use a model that can do the same work, then they can pay that person to do some more meaningful work that help get them to their goal in better way.

### Problem Statement
In this section, you will want to clearly define the problem that you are trying to solve, including the strategy (outline of tasks) you will use to achieve the desired solution. You should also thoroughly discuss what the intended solution will be for this problem. Questions to ask yourself when writing this section:
- _Is the problem statement clearly defined? Will the reader understand what you are expecting to solve?_
- _Have you thoroughly discussed how you will attempt to solve the problem?_
- _Is an anticipated solution clearly defined? Will the reader understand what results you are looking for?_

### Metrics
The goal is to be able to correctly identify the handwritten digit by applying algorithms that learn based on the training set, which is thousands of pictures of handwritten digits. I want to be able to create a model/algorithm that performs better than the baseline models. I will have to do research into neural networks and which algorithms and layers perform best for image classification. The data I will be using is a very commonly known dataset called MNIST. It contains hundreds of thousands of pictures of handwritten digits that I will be able to use to solve the problem. More information about the MNIST dataset can be found here. The training data consists of 60,000 images and the test set contains 10,000 images.

I was also able to find a similar Kaggle competition (https://www.kaggle.com/c/digit-recognizer/overview). Here you can see many people taking the challenge to classify the handwritten digits properly. 

Some models that are historically use to evaluate this dataset are SVM and k-nearest neighbors. I will use these 2 models as a baseline for my work, and then hopefully I create and fine tune a model that will perform even better than these baselines. K-nearest neighbor is good fit for this problem since its goal is to essentially cluster the alike images into the same cluster. This helps me because it’s choosing the images that most likely are the same as those in that same cluster. For me, I can make those clusters each of the different digits 0-9. Then when it’s predicting, it will choose the cluster that the digit resembles the most. In order to evaluate the performance of the model I create, I will evaluate the accuracy. This will tell me the percentage of photos that were correctly classified as the right digit. We only care about when our model is correctly classifying images so that’s why I chose accuracy as the evaluation metric.



## II. Analysis

### Data Exploration
At first, I found the Kaggle competition and started by using the data that they provided directly. Once reading in the data, I quickly found out that the test data did not have any labels for it. This is because for the competition you are supposed to submit your best model and they will run it against the test data’s labels to calculate accuracy for you. That way the answer isn’t out there. But for this project, I will need the test labels, so I decided to do some research and see if I can find the data from another source. I was able to find out the the MNIST dataset was actually preloaded into the keras module. All I had to do was import it like I would any other library to use it. So that was how I actually got the data used in my analysis. I will say there were some slight differences in the datasets being that they came from 2 different sources. From Kaggle, each row represented an image and each column represented the pixel in the image. I was able to read it into a pandas dataframe just like that. That means if I wanted to use the Kaggle data, I would need to transform the dataframe into an array of arrays. On the other hand, using the data from keras, it came already packaged as an array of arrays. Also, they took it a step further and it’s already been pre-processed a bit in the sense that they reshaped the images to represent the size 28x28. That is also fine, but if we need to return to the original size, we just have to do a bit of manipulating. I did have to return to the original size so you will find the code to go between the 2 sizes in the notebook. I needed to do this because the algorithms expected 2D inputs, not the 3 dimensions that come with reshaping the images. Another preprocessing step that was done was transforming the X-data into floats and the labels into integers. This just makes handling the pixels easier and keeps the labels as whole numbers (no decimals). Since we have 10 different integers as the labels, we can one-hot encode these to make it easier to handle when feeding it into the model. Originally I thought I was going to need to reshape the images again to have a single channel on top of being resized to 28x28, but then realized I did not as the models can't intake dimensions higher than 2.

### Exploratory Visualization
I started off by first exploring some of the images that I was going to try classifying. We can see that the images are pretty easy to classify to a human eye, but since they are a bit odd shaped sometimes, I can see how a computer or algorithm might have a bit of difficulty. When visualizing the images, notice we have to use the reshaped images (28x28). This is so that we give it the 2D affect which allows us to plot the image's pixels. I thought it was important to get an idea of what the handwritten samples look like before deciding the preprocessing steps and defining the model architecture.

### Algorithms and Techniques
In order to solve this problem, I will implement a k-nearest neighbor model that’s tuned so that it can classify the images properly. I feel that it best suites the problem at hand. I think choosing a k=10 as there are 10 numbers (0-9) makes the most sense, but we will see once we do more analysis.

In this section, you will need to discuss the algorithms and techniques you intend to use for solving the problem. You should justify the use of each one based on the characteristics of the problem and the problem domain. Questions to ask yourself when writing this section:
- _Are the algorithms you will use, including any default variables/parameters in the project clearly defined?_
- _Are the techniques to be used thoroughly discussed and justified?_
- _Is it made clear how the input data or datasets will be handled by the algorithms and techniques chosen?_

### Benchmark
Some models that are historically use to evaluate this dataset are SVM and k-nearest neighbors. I will use these 2 models as a baseline for my work, and then hopefully I create and fine tune a model that will perform even better than these baselines. K-nearest neighbor is good fit for this problem since its goal is to essentially cluster the alike images into the same cluster. This helps me because it’s choosing the images that most likely are the same as those in that same cluster. For me, I can make those clusters each of the different digits 0-9. Then when it’s predicting, it will choose the cluster that the digit resembles the most.

In this section, you will need to provide a clearly defined benchmark result or threshold for comparing across performances obtained by your solution. The reasoning behind the benchmark (in the case where it is not an established result) should be discussed. Questions to ask yourself when writing this section:
- _Has some result or value been provided that acts as a benchmark for measuring performance?_
- _Is it clear how this result or value was obtained (whether by data or by hypothesis)?_


## III. Methodology
_(approx. 3-5 pages)_

### Data Preprocessing
In this section, all of your preprocessing steps will need to be clearly documented, if any were necessary. From the previous section, any of the abnormalities or characteristics that you identified about the dataset will be addressed and corrected here. Questions to ask yourself when writing this section:
- _If the algorithms chosen require preprocessing steps like feature selection or feature transformations, have they been properly documented?_
- _Based on the **Data Exploration** section, if there were abnormalities or characteristics that needed to be addressed, have they been properly corrected?_
- _If no preprocessing is needed, has it been made clear why?_

### Implementation
In this section, the process for which metrics, algorithms, and techniques that you implemented for the given data will need to be clearly documented. It should be abundantly clear how the implementation was carried out, and discussion should be made regarding any complications that occurred during this process. Questions to ask yourself when writing this section:
- _Is it made clear how the algorithms and techniques were implemented with the given datasets or input data?_
- _Were there any complications with the original metrics or techniques that required changing prior to acquiring a solution?_
- _Was there any part of the coding process (e.g., writing complicated functions) that should be documented?_

### Refinement
In this section, you will need to discuss the process of improvement you made upon the algorithms and techniques you used in your implementation. For example, adjusting parameters for certain models to acquire improved solutions would fall under the refinement category. Your initial and final solutions should be reported, as well as any significant intermediate results as necessary. Questions to ask yourself when writing this section:
- _Has an initial solution been found and clearly reported?_
- _Is the process of improvement clearly documented, such as what techniques were used?_
- _Are intermediate and final solutions clearly reported as the process is improved?_


## IV. Results
_(approx. 2-3 pages)_

### Model Evaluation and Validation
In this section, the final model and any supporting qualities should be evaluated in detail. It should be clear how the final model was derived and why this model was chosen. In addition, some type of analysis should be used to validate the robustness of this model and its solution, such as manipulating the input data or environment to see how the model’s solution is affected (this is called sensitivity analysis). Questions to ask yourself when writing this section:
- _Is the final model reasonable and aligning with solution expectations? Are the final parameters of the model appropriate?_
- _Has the final model been tested with various inputs to evaluate whether the model generalizes well to unseen data?_
- _Is the model robust enough for the problem? Do small perturbations (changes) in training data or the input space greatly affect the results?_
- _Can results found from the model be trusted?_

### Justification
In this section, your model’s final solution and its results should be compared to the benchmark you established earlier in the project using some type of statistical analysis. You should also justify whether these results and the solution are significant enough to have solved the problem posed in the project. Questions to ask yourself when writing this section:
- _Are the final results found stronger than the benchmark result reported earlier?_
- _Have you thoroughly analyzed and discussed the final solution?_
- _Is the final solution significant enough to have solved the problem?_


## V. Conclusion
_(approx. 1-2 pages)_

### Free-Form Visualization
In this section, you will need to provide some form of visualization that emphasizes an important quality about the project. It is much more free-form, but should reasonably support a significant result or characteristic about the problem that you want to discuss. Questions to ask yourself when writing this section:
- _Have you visualized a relevant or important quality about the problem, dataset, input data, or results?_
- _Is the visualization thoroughly analyzed and discussed?_
- _If a plot is provided, are the axes, title, and datum clearly defined?_

### Reflection
In this section, you will summarize the entire end-to-end problem solution and discuss one or two particular aspects of the project you found interesting or difficult. You are expected to reflect on the project as a whole to show that you have a firm understanding of the entire process employed in your work. Questions to ask yourself when writing this section:
- _Have you thoroughly summarized the entire process you used for this project?_
- _Were there any interesting aspects of the project?_
- _Were there any difficult aspects of the project?_
- _Does the final model and solution fit your expectations for the problem, and should it be used in a general setting to solve these types of problems?_

### Improvement
In this section, you will need to provide discussion as to how one aspect of the implementation you designed could be improved. As an example, consider ways your implementation can be made more general, and what would need to be modified. You do not need to make this improvement, but the potential solutions resulting from these changes are considered and compared/contrasted to your current solution. Questions to ask yourself when writing this section:
- _Are there further improvements that could be made on the algorithms or techniques you used in this project?_
- _Were there algorithms or techniques you researched that you did not know how to implement, but would consider using if you knew how?_
- _If you used your final solution as the new benchmark, do you think an even better solution exists?_

-----------

**Before submitting, ask yourself. . .**

- Does the project report you’ve written follow a well-organized structure similar to that of the project template?
- Is each section (particularly **Analysis** and **Methodology**) written in a clear, concise and specific fashion? Are there any ambiguous terms or phrases that need clarification?
- Would the intended audience of your project be able to understand your analysis, methods, and results?
- Have you properly proof-read your project report to assure there are minimal grammatical and spelling mistakes?
- Are all the resources used for this project correctly cited and referenced?
- Is the code that implements your solution easily readable and properly commented?
- Does the code execute without error and produce results similar to those reported?
