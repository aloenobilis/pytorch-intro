<img src="assets/images/pytorch-logo.png" width="800px" />
# pytorch-intro 




# Setup 
Pytorch setup - https://pytorch.org/get-started/locally/
Install via conda ```conda install pytorch torchvision -c pytorch```, note that OSX doesnt support cuda, need eGPU/Cloud GPU

# Run
Note that jupyter is configured to use SSL. In chrome navigate to "chrome://flags/#allow-insecure-localhost" to trust self signed certs. This will prompt for a SHA1 password.
~/```jupyter lab```

# Neural Networks


<p style="text-align: center;"></p>
    <img src="assets/images/neuralnetwork.png" />
</p>
<small>Fig 1: Neural Network</small>
<br/>
<br/>

Descriptive features are converted to numerical values which are used as the inputs to the neural network.
Hidden layers are called 'hidden' because we don't have control over them, we can see whats going on within them but we don't change any values within
hidden layers. 
Output in the general sense, outputs multiple numerical values and whichever one is greatest (argmax(outputs)), then that output is the prediction, for example say we have three outputs Dogs: 13, Cats: 2, Human: 21, then because human has the greatest output, we say that the prediction is a human.

Every input and neuron are connected via a line, when all inputs are connected to all neurons, we then have a Fully Connected Network. Each line/connection is really a weight. The input value is multiplied by a weight, a bias is optionally added in, a bias could be anything like 3, so ```(input * value) + 3```, the result is then passed to another neuron.

<br/>
<p style="text-align: center;"></p>
    <img src="assets/images/singleneuron.png" />
</p>
<small>Fig 2: Neuron</small>
<br/>
<br/>

A single neuron accepts multiple inputs, each input is multiplied by a weight and a bias is possibly added, then all results are summed together (&epsilon;) and then passed through an activation function (ƒ). 
The activation function is what mimics a neuron in your brain, it either fires off or doesn't is what a stepper function looks for. We'll most commonly use a sigmoid function which outputs a range from 0 to 1, which also mimics firing or not, the fact that it uses a range between 0 and 1 helps as the inputs are also between 0 and 1.


### Closing
Each of these weights and biases is what is called a parameter, if you see how many connections there are you can deduce that there are a lot of parameters, a weight and a bias is one paramater, so if we have a bias then each connection can have two parameters. The machine can modify each weight independently with the goal of fitting to our desired output, for example training a network to recognize a human in an image, if we have three outputs, Dog, Cat and Human, we would want our ouput to be ```[0,0,1]```. 

A neural network is then just a giant function where we allow the machine to tweak variables and parameters to output desired results.


# MNIST
<br/>
<p style="text-align: center;"></p>
    <img src="assets/images/NNinputoutput.png" width="600px"/>
</p>
<small>Fig 3: MINIST Input to Output</small>
<br/>
<br/>


# Learning Rate
<br/>
<p style="text-align: center;"></p>
    <img src="assets/images/learningrate.png" width="300px"/>
</p>
<small>Fig 4: Learning Rate</small>
<br/>
<br/>
How does the learning rate correspond to training times and how well the model will learn?


The goal with optimization is to get loss to be at the minumum point on the optimization curve. The learning rate in part, dicates the size of the step that the optimizer will take to reduce loss. Each time data passes through the NN different valued weights will generate different loss, as the data that goes through the network batch after batch, the optimizer will tweak the weights to produce the least loss so that the output contains the generalizations, this involves back propagating the loss over the model paramaters.

The learning rate step size if too big will overshoot, a too small step size will undershoot, or converge at a single point. A fixed step size will need to be correct in order to reduce loss, its up to us to tweak its value so that the loss decreases. Another way is using a decaying learning rate, so that the steps start big and become smaller.

Using the optimizer we calculate loss based on the output from the model and the desired output, then re-callibrate the weights based on the loss and repeat. So we keep feeding data through the NN reducing loss and improving accuracy. When training models, we optimize for loss which gives us more accurate models. 

Loss is calculated in a number of ways depending on the output, for example a One Hot Vector like [0, 0, 1, 0] which contains one value that is on/hot would use mean squared error. For our example, the loss is a single scaler value so nll_loss is used.

<br/>

# Convolutional Neural Networks
<br/>
<p style="text-align: center;"></p>
    <img src="assets/images/cnn.jpeg" width="600px"/>
</p>
<small>Fig 4: Convolutional Neural Network</small>
<br/>
<br/>


Cats & Dogs Dataset - https://www.microsoft.com/en-us/download/details.aspx?id=54765

With regards to Pytorch, a CNN is another layer within the NN layers such as the fully connected linear layers.

CNN's were traditionally used for image related tasks but in recent years have outperformed RNN's on seqeuntial data tasks.

CNN's accept 2d or even 3 dimensional input, which means we can pass images directly in, without having to 'flatten' the data as with our NN-MNIST model. (CNN's for example can be used to detect lung cancer where the scans are in 3d).

We take an image, which is just made up of pixels, and apply a convolution over the image with its goal being to locate features. A convolution will 'scan' parts of the image in a window over the image, this window is called a kernal, the kernal scans the image and looks for features within its window (ex 3px by 3px window). As the image passes through the network, each convolutions' feature detection builds on the previous one, for example first edges or curves are recognized and then cicles or sqaures and then houses or cars etc, each builds on the other. So the kernal slides its window over the image to detect features, essentially breaking down the image into smaller chunks, then it outputs an 'image' that contains the features in the form 'numerical correlation to feature type'. The output image is then pooled, which also has a window, max pooling basically takes the maximum value in each window, this outputs a list of features in numerical form...



