# Introduction
"Jigsaw Unintended Bias in Toxicity Classification" is contest to detect toxicity among online comments. This is a bit different that usual classification as it has to detect toxicity in a non biased way ie. figure out when identity nouns are used for toxicity and when not.

The train data has the comment and some identity fields for reference. The task is to detect if the comments are toxic or not.

# Approach

## Pre-processing

At first the data is split among identity columns and the input texts. Then a built in BERT pre-processor is used as here a vanilla implementation of BERT is used for the classification.

## Model Building and Training

Here, I have used BERT model as its performance is great for text classification tasks. Ther version I have used is small bert (bert_en_uncased_L-2_H-256_A-4), which has 2 hidden layers, 256 hidden units and 4 attention heads. Considering space and time constraints, this was good for this task. Along with this I have also used a bert pre-processor that would process the texts into desired format for training.

The model consists of Bert model -> "Pooled Outputs" -> Dropout layer -> Dense Layer. The bert had to be kept un-trainable for computational costs, so only the output layer will get trained.

The loss is BinaryCrossEntropy as it is a binary classification problem, and the metric is BinaryAccuracy.

The model was run for 3 epochs, using adam optimizer. Epoch count had to be kept short because of computational cost.

# Result

After training, the model had an accuracy of 70%. It is pretty low, but considering almost no training, this performed pretty well.


