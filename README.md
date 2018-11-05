# multilabel-MXNet
**This is the implementation of the multilabel image classificaton in MXNet. Multilabel means each image belong to 1 or more labels and it is different from multi task.**

**This implementation doesn't need to recompile MXNet and is very convenient for you to use. Firstly, I assume that you can use MXNet normally. Then, do as follows:**

## Data
If you are doing a single label image classification, your .lst file may like this:

|ID	|label   |      image_name|
|:------|:-------|:---------------| 
|5247	|0.000000|	image1.jpg|
|33986	|1.000000|	image2.jpg|
|39829	|2.000000|	image3.jpg|
|15647	|3.000000|	image4.jpg|
|10369	|1.000000|	image5.jpg|
|22408	|3.000000|	image6.jpg|
|2598	|2.000000|	image7.jpg|

For multilabel image classification, you should create `.lst` file like `multilabel-MXNet/data_example/train_data.lst` (take 4 classes as example)


**In this implementation, we only use `.lst` and raw images as the input instead of `.rec` file.**


## Train
 `run_train.sh` is the train script for you to start fine-tune quickly. You should open this script and change the path of `train_multilabel.py`, `.lst` file, imagefile and model-prefix after you clone the project.

   Then run: 
```
sh run_train.sh
```

## More details

* `--num-classes` 8 in `run_train.sh` means the maximum number of label is 8 classes. For example, iamge1 has label 1,5; image2 has label 1,2,3; image3 has label 1. You can change the number for your data.

* In the `train_multilabel.py`, I use `net = mx.symbol.sigmoid(data=net, name='sig')` and `net = mx.symbol.Custom(data=net,name='softmax', op_type='CrossEntropyLoss')` instead of `mx.symbol.softmaxOutput` to deal with multilabel problem. sigmoid layer take the output of full connection as input and translate it into (0,1), which means the probability. CrossEntropy layer take the probability (0,1) as input and calculate the loss.


