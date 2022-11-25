# Gradcamsupervised
My personal project into using cam for identifying areas to cutout from data set to train models
Due to computing limitations I am only running on CIFAR10 and resnet18, feel free to scale up training
The code for cutout + supervised is to generate the comparison for baseline as well as generate a trained resnet18 supervised model
CAM exclusion is then for the actual training type I want to test
Most of the idfference comes through transformation for supervised learning
Using torchcam extract a tensor that represents the focus of the model, however due to limitations of torch cam tensor is 4by 4 not 32 by 32.
Then treating  focus tensor as a probability matrix remove portions of image with the most likely to be removed parts being those of highest focus.
Due to the nature of this transformation being none random and having to be done before most other transformations, I had to write a subclass to edit getitem to apply cutout before actual transformations.
Also focus tensors done beforehand due to limitations of cam being very slow therefore I do not want to repeat extracting focus.
