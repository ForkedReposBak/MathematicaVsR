# Deep learning examples

## Introduction

This project is for the comparison of the Deep Learning functionalities in R/RStudio and Mathematica/Wolfram Language (WL).

The project is aimed to mirror and aid the talk 
["Deep Learning series (session 2)"](https://www.meetup.com/Orlando-MLDS/events/250086544/)
of the meetup
[Orlando Machine Learning and Data Science](https://www.meetup.com/Orlando-MLDS).

The focus of the talk is R and Keras, so the project structure is strongly influenced by the content 
of the book [Deep learning with R](https://www.manning.com/books/deep-learning-with-r), 
\[[1](https://www.manning.com/books/deep-learning-with-r)\], and 
the corresponding Rmd notebooks, \[[2](https://github.com/jjallaire/deep-learning-with-r-notebooks)\].

Some of Mathematica's notebooks repeat the material in \[[2](https://github.com/jjallaire/deep-learning-with-r-notebooks)\]. 
Some are original versions.

WL's Neural Nets framework and abilities are fairly well described in the 
reference page 
["Neural Networks in the Wolfram Language overview"](http://reference.wolfram.com/language/tutorial/NeuralNetworksOverview.html), \[4\],
and the [webinar talks](http://www.wolfram.com/broadcast/c?c=442) \[5\].

The corresponding documentation pages 
\[[3](https://keras.rstudio.com/reference/index.html)\] (R) and 
\[[6](http://reference.wolfram.com/language/guide/NeuralNetworks.html)\] (WL) 
can be used for a very fruitful comparison of features and abilities.

**Remark:** With "deep learning with R" here we mean "Keras with R". 

**Remark:** An alternative to R/Keras and Mathematica/MXNet is the library 
[H2O](https://www.h2o.ai) (that has interfaces to Java, Python, R, Scala.) See project's directory 
[R.H2O](https://github.com/antononcube/MathematicaVsR/tree/master/Projects/DeepLearningExamples/R.H2O) 
for examples.


## The presentation

- [Mind map for the presentation](https://github.com/antononcube/MathematicaVsR/blob/master/Projects/DeepLearningExamples/Diagrams/Deep-learning-with-Keras-in-R-mind-map.pdf).
*(Has life hyperlinks.)*

- Presentation slideshow: 
  [html](http://htmlpreview.github.io/?https://github.com/antononcube/MathematicaVsR/blob/master/Projects/DeepLearningExamples/R/Keras-with-R-talk-slideshow.html#/),
  [Rpres](https://github.com/antononcube/MathematicaVsR/blob/master/Projects/DeepLearningExamples/R/Keras-with-R-talk-slideshow.Rpres).

- ["Neural network layers primer" slideshow](https://github.com/antononcube/MathematicaVsR/blob/master/Projects/DeepLearningExamples/Mathematica/Neural-network-layers-primer.pdf).

  - The slideshow is part of [Sebastian Bodenstein's presentation at Wolfram U](http://www.wolfram.com/broadcast/video.php?c=442&v=2173).     
  *(It was separated/extracted for clarity and convenience during the meetup presentation.)*

- Recording of the presentation at YouTube:   
  [ORLMLDS Deep learning series (2): "Using Keras with R (... and MXNet with WL)"](https://youtu.be/AidENXetn3o).
    
  - Corrections to some of the bloopers.
   
    1. At 7:01 the correct statement is "5000 for training and 1000 for testing (handwritten images)". 
    
    2. The Mathematica neural network at 20:10 has some transpositions, 
    the correct Mathematica netwoirk corresponding to the R-Keras one is given in 
    [this notebook](https://github.com/antononcube/MathematicaVsR/blob/master/Projects/DeepLearningExamples/Mathematica/Simple-neural-network-classifier-over-MNIST-data.pdf).
    
    3. At 20:22 the correct statement is "Mathematica provides very nice visualization..."; (not R). 

- The info-chart 
["Classification of handwritten digits by matrix factorization"](https://github.com/antononcube/MathematicaVsR/blob/master/Projects/DeepLearningExamples/Diagrams/Classification-of-handwritten-digits-by-MF.pdf) 
(used in the presentation.)

## The big picture

Deep learning can be used for both supervised and unsupervised learning. 
***In this project we concentrate on supervised learning.*** 

The following diagram outlines the general, simple classification workflow we have in mind.

[![simple_classification_workflow](https://imgur.com/OT5Qkqil.png)](https://imgur.com/OT5Qkqi.png)

Here is a corresponding classification [monadic pipeline](https://en.wikipedia.org/wiki/Monad_(functional_programming)) 
in Mathematica:

![monadic_pipeline](https://imgur.com/zwjBynL.png)

## Code samples

R-Keras uses monadic pipelines through the library [`magrittr`](https://github.com/tidyverse/magrittr). 
For example:

    model <- keras_model_sequential() 
    model %>% 
      layer_dense(units = 256, activation = 'relu', input_shape = c(784)) %>% 
      layer_dropout(rate = 0.4) %>% 
      layer_dense(units = 128, activation = 'relu') %>%
      layer_dropout(rate = 0.3) %>%
      layer_dense(units = 10, activation = 'softmax')

The corresponding Mathematica command is:

    model =
     NetChain[{
       LinearLayer[256, "Input" -> 784],
       ElementwiseLayer[Ramp],            
       DropoutLayer[0.4],
       LinearLayer[128],
       ElementwiseLayer[Ramp],            
       DropoutLayer[0.3],
       LinearLayer[10]
     }]

## Comparison 

### Installation

- Mathematica

  - The neural networks framework comes with Mathematica. (No additional installation required.)

- R

  - Pretty straightforward using the directions in \[3\]. (A short list.)

  - Some additional Python installation is required. 

### Simple neural network classifier over [MNIST data](http://yann.lecun.com/exdb/mnist/)

- Mathematica: 
[Simple-neural-network-classifier-over-MNIST-data.pdf](https://github.com/antononcube/MathematicaVsR/blob/master/Projects/DeepLearningExamples/Mathematica/Simple-neural-network-classifier-over-MNIST-data.pdf)

- R-Keras: 
[Keras-with-R-talk-introduction.nb.html](http://htmlpreview.github.io/?https://github.com/antononcube/MathematicaVsR/blob/master/Projects/DeepLearningExamples/R/Keras-with-R-talk-introduction.nb.html),
[Keras-with-R-talk-introduction.Rmd](https://github.com/antononcube/MathematicaVsR/blob/master/Projects/DeepLearningExamples/R/Keras-with-R-talk-introduction.Rmd).


### Vector classification

*TBD...*

### Categorical classification

*TBD...*

### Regression

- Mathematica: 
[Predicting-house-prices-a-regression-example.pdf](https://github.com/antononcube/MathematicaVsR/blob/master/Projects/DeepLearningExamples/Mathematica/Predicting-house-prices-a-regression-example.pdf).

- R-Keras:
[3.6-predicting-house-prices.nb.html](https://jjallaire.github.io/deep-learning-with-r-notebooks/notebooks/3.6-predicting-house-prices.nb.html),
[3.6-predicting-house-prices.Rmd](https://github.com/jjallaire/deep-learning-with-r-notebooks/blob/master/notebooks/3.6-predicting-house-prices.Rmd).
 
  - *(Those are links to notebooks in \[2\].)*
  
### Encoders and decoders

The Mathematica encoders (for neural networks and generally for machine learning tasks) are very well designed 
and with a very advanced development.

The encoders in R-Keras are fairly useful but not was advanced as those in Mathematica.

*[TBD: Encoder correspondence...]* 

### Dealing with over-fitting

- Mathematica: 
[Training-Neural-Networks-with-Regularization.pdf](https://github.com/antononcube/MathematicaVsR/blob/master/Projects/DeepLearningExamples/Mathematica/Training-Neural-Networks-with-Regularization.pdf).

- R-Keras:
[Training-Neural-Networks-with-Regularization.nb.html](http://htmlpreview.github.io/?https://github.com/antononcube/MathematicaVsR/blob/master/Projects/DeepLearningExamples/R/Training-Neural-Networks-with-Regularization.nb.html),
[Training-Neural-Networks-with-Regularization.Rmd](https://github.com/antononcube/MathematicaVsR/blob/master/Projects/DeepLearningExamples/R/Training-Neural-Networks-with-Regularization.Rmd).

### Repositories of pre-trained models

- Mathematica: 
[Wolfram Research repository of neural networks](http://resources.wolframcloud.com/NeuralNetRepository);
can import externally trained networks in 
[MXNet](http://reference.wolfram.com/language/ref/format/MXNet.html) 
format.

- R-Keras: has commands loading for pre-trained models, \[[3](https://keras.rstudio.com/reference/index.html)\].   

### Documentation
 
- Mathematica: ["Neural Networks guide"](http://reference.wolfram.com/language/guide/NeuralNetworks.html).   

- R-Keras: ["Keras reference"](https://keras.rstudio.com/reference/index.html), 
  [cheatsheet](https://github.com/rstudio/cheatsheets/raw/master/keras.pdf).

## References

\[1\] F. Chollet, J. J. Allaire, [Deep learning with R](https://www.manning.com/books/deep-learning-with-r), (2018).

\[2\] J. J. Allaire, [Deep Learing with R notebooks](https://github.com/jjallaire/deep-learning-with-r-notebooks), (2018), GitHub.

\[3\] RStudio, [Keras reference](https://keras.rstudio.com/reference/index.html).

\[4\] Wolfram Research, ["Neural Networks in the Wolfram Language overview"](http://reference.wolfram.com/language/tutorial/NeuralNetworksOverview.html).

\[5\] Wolfram Research, ["Machine Learning Webinar Series"](http://www.wolfram.com/broadcast/c?c=442).
 
\[6\] Wolfram Research, ["Neural Networks guide"](http://reference.wolfram.com/language/guide/NeuralNetworks.html).   

