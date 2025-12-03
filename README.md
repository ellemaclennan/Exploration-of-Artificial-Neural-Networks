# Exploration-of-Artificial-Neural-Networks
In this repository I explore the effects of different design choices on a simple ANN. 

To run this notebook, clone the repository locally. Open the code in your favourite editor and simply select run all!

# Architecture choices

## Classification dataset:

  For my classification dataset I implemented 2 layers. The first layer
with 128 Neurons and the second with 64 neurons. When designing the
network I experimented with 64 and 32 neurons for the first and second
layer, respectively, but I saw a decrease in accuracy and an increase in
loss. I chose the learning rate, decay, and momentum values based on
what we saw in lecture and I observed fairly high accuracy and low loss.
For my activation function I chose ReLU. I ran the ANN with sigmoid
activation instead since I read that it is usually a good option for
binary classification, however, I noticed that the model was plateauing
and returning a decreased accuracy and increased loss so I decided to
keep using ReLU instead. I implemented dropout after the first layer
since you usually want to implement it in deeper layers where
overfitting is more likely. However, because we have such a small
dataset I don't think the placement would have a significant impact in
this case.

## Regression dataset:

For my regression dataset I implemented 2 layers. The first layer had
128 neurons and the second had 64. I experimented with adding a third
layer with 16 and then 32 neurons but in both cases my MAE and loss were
increased so I decided to keep my 2 initial layers instead. I had to
decrease my learning rate, decay and momentum because my model's loss
and mae were very high. I brought the learning rate from 0.2 down to
0.001, I kept decay the same, and I change my momentum to 0.5. For my
activation function, I used ReLU for the first two layers and Linear
activation for my output layer since that's what we used in tutorial,
and because it allows the model to output values across the entire real
number range. Again, I implemented dropout after the first layer to
avoid overfitting.

## Dropout Implementation:

  To implement dropout, I created another class called Layer_Dropout that
takes in the output of the previous layer and also an indication of
whether or not the model is in training because you don't want to apply
dropout when testing your model. The forward method assigns each element
to 1(keep the neuron) or 0(drop the neuron) based on the fraction that
you've decided to drop (i.e. 20 or 30%). The backward pass takes in the
values from the preceding layer and multiplies them by the same random
binomial generator used in the forward pass to make sure that only the
gradients from the trained neurons are input back into the previous
layer.

## Training performance: 

*The resultant training plot for the classification dataset can be found in the notebook output.*  

The classification training plot shows that as the model learns over the course of many epochs,
the accuracy is increasing and the loss is decreasing. This tells us
that the model is learning correctly. We see the learning rate decay too
which means the model is starting to take smaller steps to avoid
overshooting the minimum.  


*The resultant training plot for the regression dataset can be found in the notebook output.*  

The regression training plot shows that as the model learns over the course of many epochs,
both the MAE and loss are decreasing. This tells us that the model is
learning correctly. Similarly to our classification model, we see the
learning rate decay too which means the model is starting to take
smaller steps as it is approaching the optimal minimum.

## Results and key insights:

*The Crossentropy graphs and confusion matrices for my
classification model running on training vs testing sets can be found in the notebook output*   

The accuracy for my test set was actually higher than for my training
set which means that we did not end up overfitting and that the model is
able to accurately handle novel data which is a good indication that it
has actually learned. The cross entropy isn't great for class number 1
on the training set but the model seems fairly confident about its
ability to classify class number 0, and it makes sense that its
confidence would decrease on an unseen dataset.  

For my regression model, we see MAE and loss values of 0.130 and 0.26
for the training set. When run on the test data, we see MAE and loss
values of 0.121 and 0.023. A decrease in MAE and loss for the test set
vs the training set is promising because we can see that our model
performs well on new data. This tells us that we did not overfit!  

**Some observations:**

-   50/50 training to test split ratio caused the model to plateau on
    the first epoch and decreased accuracy and increased loss

-   Increasing the number of features even by only 2 increased the
    accuracy and decreased the loss\

-   Using a dataset with correlation increased the accuracy and
    decreased the loss

-   Doubling the number of datapoints increased training accuracy and
    decreased test accuracy very slightly but decreased loss for both
    datasets.

