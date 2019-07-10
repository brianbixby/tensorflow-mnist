# Omni-Supervised Learning with Tensorflow

A Tensorflow notebook that utilizes omni-supervised learning to model the Mnist dataset.

### What is Omni-Supervised Learning?

Omni-supervised learning is a special regime of semi-supervised learning in which a learner exploits all labeled data plus internet-scale sources of unlabeled data. This project is an implementation of [Facebook's scholarly article](https://arxiv.org/pdf/1712.04440.pdf) with the Mnist dataset.

Facebook believes that an Omni-supervised model's lower bounds is the accuracy of training on the initial labeled data and success should be evaluated by how for a model surpasses this baseline. 

### Results and Methodology

Using the methodologies outlined in the research paper mentioned above I was able to increase my model's accuracy on validation data from 94.95% to 96.69%.

I broke my dataset into training data(4,200 examples), validation data(4,200 examples) and unlabeled data(33,600 examples). From here I normalized my data and built a Teacher and Student model. I used fully supervised learning to train my Teacher model with the labeled training data then I used this model to make predictions on the unlabeled data. If my model was more than 99.999% confident with a prediction I moved that example to the newly-labeled data dataset. Next, I gave my student model both the training data and the newly-labeled data(60% training data and 40% newly-labeled data per batch). The training model applies 2 transformations on each example(a rotation and a crop) as it trains. My student model then made predictions on the unlabeled data and just as before with the Teacher model if it was more than 99.999% confident of a prediction then I move that example to the newly-labeled data dataset. At this point, I combine the newly-labeled data into the training data and repeat the process resetting the weights of both models each time.

[View the Notebook here](https://github.com/brianbixby/tensorflow-mnist/blob/master/mnist_semi_supervised.ipynb)