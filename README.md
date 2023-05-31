[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-c66648af7eb3fe8bc4f294546bfd86ef473780cde1dea487d3c4ff354943c9ae.svg)](https://classroom.github.com/online_ide?assignment_repo_id=10443650&assignment_repo_type=AssignmentRepo)
# Building baseline classifiers on the Cifar10 dataset

## Description
This repository includes two scripts. The first script performs Logistic Regression classification and the second trains a MLPClassifier. Both scripts will also save a classification report as well as the trained model. 

The classifiers will be trained on the Cifar10 dataset. The CIFAR-10 dataset consists of 60000 32x32 colour images in 10 classes, with 6000 images per class. More information about the dataset can be found on the following link:
https://www.cs.toronto.edu/~kriz/cifar.html


The repository has the following structure:

| name | description |
| --- | --- |
| models | folder for the saved models |
| report | folder for the classification reports |
| src | folder which contains the two scripts |
| requirements | txt file listing the necessary packages required to run the scripts |
| run_logreg.sh | shell file which the user may use in order to run the logistic regression classifier |
| run_mlpclf.sh | shell file which the user may use in order to run the MLP classifier |
| setup.sh | shell file which opens a virtual enviroment and installs the packages listed in the requirements file |

## User instructions
In order to train and save the two models, three shell files need to be run like so:

1. install packages using setup file

`bash setup.sh`

(opens virtual enviroment. Installs the necessary packages)

2. train logistic regression classifier

`bash run_logreg.sh`

(trains a logistic regression classifier on Cifar10 dataset. Saves model and classification report)

3. train MLP classifier

`bash run_mlpclf.sh`

(trains a MLP classifer on Cifar10 dataset. Saves model and classification report)

## Discussion of results 

### Classification report for logistic regression classifier:

              precision    recall  f1-score   support

    airplane       0.34      0.39      0.36      1000
    automobile     0.38      0.37      0.38      1000
    bird           0.28      0.19      0.22      1000
    cat            0.24      0.12      0.16      1000
    deer           0.24      0.21      0.23      1000
    dog            0.30      0.31      0.30      1000
    frog           0.28      0.36      0.31      1000
    horse          0.31      0.33      0.32      1000
    ship           0.35      0.40      0.37      1000
    truck          0.38      0.47      0.42      1000

    accuracy                           0.32     10000
    macro avg      0.31      0.32      0.31     10000
    weighted avg   0.31      0.32      0.31     10000

### Classification report for MLP classifier

              precision    recall  f1-score   support

    airplane       0.38      0.41      0.40      1000
    automobile     0.40      0.49      0.44      1000
    bird           0.26      0.34      0.30      1000
    cat            0.28      0.11      0.16      1000
    deer           0.27      0.26      0.27      1000
    dog            0.33      0.34      0.34      1000
    frog           0.28      0.29      0.28      1000
    horse          0.45      0.39      0.42      1000
    ship           0.44      0.44      0.44      1000
    truck          0.42      0.47      0.44      1000

    accuracy                           0.35      10000
    macro avg       0.35      0.35     0.35      10000
    weighted avg    0.35      0.35     0.35      10000

The classification reports show that the MLP classifier outperforms the logistic regression classifier on nearly all fronts. When looking at the f1-score, which can be defined as the harmonic mean between precision and recall, there is an increase from 0.32 to 0.35. It also appears that "cat" is the class that is hardest to predict for both classifiers.

The MLP (Multi-layer Perceptron) is a more complex classifier consisting several nodes in hidden layers. The MLP model in this script consists has two hidden layers with 64 and 10 nodes respectively. An MLP can therefore consist of multiple neurons that have the architecture of an logistic regression classifier (the model in this repository uses an relu function as opposed to the sigmoid function, however).

In order to improve the results of the MLP classifier, one possibility might be to increase the number or iterations (how many times the weights are updated). However, when increasing the number of iteration you also risk overfitting the model, so that it perform well on the training data but more poorly on the test data. One way of checking overfitting by observing the loss during training. If the loss starts stagnating or increasing it is a sign that the model may be overfit.
It could also be possible to increase the number of hidden layers. Although, it is generally not necessary to have more than three hidden layers in a neural network.

I decided to try experimenting with the model by increasing the number of hidden layers from 2 to 3 (64, 22, 10). I also changed the number of iterations from 20 to 35. I also tried with 40 but the avg F1-score seemed to be getting lower. But maybe that is due to the fact that there can be changes of performances between runs.  That being said, by making these changes the avg f1-score was increased from 0.35 to 0.40 :

              precision    recall  f1-score   support

    airplane       0.41      0.45      0.43      1000
    automobile     0.49      0.44      0.46      1000
    bird           0.34      0.31      0.32      1000
    cat            0.33      0.21      0.26      1000
    deer           0.32      0.33      0.33      1000
    dog            0.44      0.32      0.37      1000
    frog           0.36      0.46      0.40      1000
    horse          0.41      0.49      0.45      1000
    ship           0.45      0.51      0.48      1000
    truck          0.44      0.47      0.46      1000

    accuracy                           0.40     10000
    macro avg      0.40      0.40      0.40     10000
    weighted avg   0.40      0.40      0.40     10000

If the results does not improve further with more itererations, then perhaps using a more complex model such as the pretrained model VGG16 would be beneficial.
