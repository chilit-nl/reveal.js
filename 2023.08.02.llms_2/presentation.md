# Large Language Models 
### Part 2 - Building a language model

![ChatGPT](ChatGPT.png "ChatGPT")

----

## Contents

- Welcome and Introduction <!-- .element: class="fragment" -->
- Quick Review of Previous Session <!-- .element: class="fragment" -->
- A Dive into Language Models <!-- .element: class="fragment" -->

Note:

Welcome everyone to our session. We'll begin by quickly reviewing what we discussed last time on neural networks, and then dive into our main topic for today - Large Language Models and text prediction.

----

### Review of Previous Session

- Basics of Neural Networks <!-- .element: class="fragment" -->
- Training Neural Networks with Gradient Descent <!-- .element: class="fragment" -->
- Handwritten Digit Classification Problem <!-- .element: class="fragment" -->

Note:

To recap our last session, we covered how neural networks work, and how we can train them using Gradient Descent. We also looked at the application of this training to the famous handwritten digit classification problem.

--- -

### Language Models: Introduction

- Definition of Language Models <!-- .element: class="fragment" -->
- Application of Language Models <!-- .element: class="fragment" -->

Note:

Now, let's introduce language models. Simply put, these are types of models that can predict the next word in a sentence, based on the words that have come before it. They have applications ranging from translation, autocorrect, to creating AI like ChatGPT.

----


## LSTM and Tokenization

- Introduction to LSTM and its advantages <!-- .element: class="fragment" -->
- The role of Tokenizers in NLP <!-- .element: class="fragment" --> 

Note:

Today we'll focus on a type of recurrent neural network called Long Short-Term Memory or LSTM. These have an advantage in processing sequences of data with long-term dependencies. To prepare our text data for LSTM, we use something called a tokenizer, which converts our text into numerical data that the model can understand.

---

## Text Prediction using LSTM

- Project Overview: Text prediction using LSTM <!-- .element: class="fragment" -->
- Data Source: WhatsApp chat history <!-- .element: class="fragment" -->

Note:

I have prepared a project where we use LSTM to create a text predictor. Our training data is the WhatsApp chat history between me and my girlfriend. Let's see how we can create a language model that can predict text in our personal chat conversations.

---

### Understanding LSTMs

- Concept of Recurrent Neural Networks (RNNs) <!-- .element: class="fragment" -->
- Problem with Traditional RNNs <!-- .element: class="fragment" -->
- Introduction of LSTMs <!-- .element: class="fragment" -->

Note:

Before diving into LSTMs, let's briefly revisit Recurrent Neural Networks (RNNs). RNNs excel at processing sequence data but suffer from the problem of long-term dependencies. LSTMs were introduced to combat this problem and can remember important information while forgetting irrelevant details.

---

### Architecture of LSTM

- Cell State
- Forget Gate
- Input Gate
- Output Gate

Note:

The LSTM has a unique structure compared to traditional neural networks. It consists of a cell state and three "gates". The cell state carries information through the network. The forget gate decides what information to discard from the cell state. The input gate decides what new information to store in the cell state. The output gate decides what information to output based on input and the current cell state.

---

### LSTM vs Traditional RNNs

- Handling of Long-Term Dependencies
- Gradients and the Vanishing Gradient Problem
- Real-World Applications

Note: 

LSTMs handle long-term dependencies better than traditional RNNs, thanks to their unique architecture. They also overcome the problem of vanishing gradients, making them more effective at learning from training data. That's why LSTMs have been used in a variety of real-world applications, from speech recognition to anomaly detection in network traffic.

---

### LSTM in NLP

- Sequential Nature of Language
- LSTM in Text Generation and Prediction

Note:

Language is inherently sequential, which makes LSTMs ideal for NLP tasks. Particularly in text generation and prediction, LSTMs can capture the context and dependencies between words in a sentence, making the generated text more coherent and contextually relevant.

----

### Project Implementation

- Data Preparation
- Building the Model
- Training and Testing the Model
- Results and Analysis

Note:

We'll go through the steps of preparing our data, building our LSTM model, training and testing it, and finally analyzing the results.

---

### Improvement Areas for Text Prediction Model

- Larger Dataset
- Model Complexity
- Hyperparameter Tuning
- Stop characters

Note:

Our model's performance can be improved in several ways. Firstly, we can use a larger dataset to give the model more context and variation in text to learn from. Secondly, we could increase model complexity by adding more layers or using a more complex model, like a transformer-based model. Lastly, fine-tuning hyperparameters such as the learning rate, batch size, and number of epochs can lead to better results.

---

### Exploring Other Models and Techniques

- Transformer Models
- Attention Mechanism
- Pretrained Models

Note: 

There are other models and techniques we could consider for improving our text prediction. Transformer models, for example, have shown excellent performance in NLP tasks. The attention mechanism, which gives different importance to different words in a sentence, could provide better context understanding. Lastly, using pretrained models like GPT-3 or BERT could significantly boost performance, as these models have been trained on vast amounts of data.

---


### Conclusion

- Review of the session
- The power and potential of Large Language Models

Note:

To conclude, we've learned how LSTM can be used to create a text prediction model. This gives us a glimpse of the power of large language models like GPT-3, which can generate very realistic human-like text.

---

### Long Short-Term Memory (LSTM) Networks

![LSTM](types/04-LSTM.png "LSTM")

Note:

- A type of RNN with improved memory capabilities
- Overcomes the vanishing gradient problem
- Suitable for tasks involving long sequences

<hr>

- Practical example: Machine translation
- Special type of RNN 
- machine translation and text generation
- Overcome the vanishing gradient problem, which occurs when ??

---


### Autoencoders (AEs)

![AE](types/05-AE.png "AEs")

Note:

- Autoencoders: Unsupervised learning for dimensionality reduction and feature learning
- GANs: Two neural networks (generator and discriminator) competing against each other to generate realistic data

<hr>

- Practical example: denoising images, inpainting missing parts of an image, or transferring the style of one image onto another (style transfer).
- unsupervised learning neural network 
- Dimensionality reduction and feature learning. 
- encoder that compresses the input data 
- decoder that reconstructs the data from the compressed representation.

---

### Generative Adversarial Networks (GANs)

![GANs](types/06-GAN.png "GANs")

Note:

- GANs: Two neural networks (generator and discriminator) competing against each other to generate realistic data

<hr>

GANs
- Practical example: generate realistic synthetic images
- 2 neural networks, generator and the discriminator
- compete against each other. 
- The generator creates realistic data samples, while the discriminator attempts to distinguish between real and generated samples. 
- This competition leads to the generator producing increasingly realistic data.

---

### Overview NNs

- Feedforward Neural Networks (FNNs)
    - Classification
- Convolutional Neural Networks (CNNs)
    - Image processing and computer vision
- Recurrent Neural Networks (RNNs)
    - Sentiment analysis
- Long Short-Term Memory (LSTM) Networks
    - Machine translation
- Autoencoders (AEs)
    - Denoising Images, Inpainting, style transfer
- Generative Adversarial Networks (GANs)
    - Synthetic images, audio

--- 

![types](types/types.png "types")

----

### Neural network

![neuron](neuron.png "neuron")

Note:
- Artificial neurons: Inspired by biological neurons
- Dendrites from other neurons
- Via Axon
- Splits into synapses (connect to other dendrites)
- Connects to other neurons

---

### Neural network

![network](network.png "network")

- Input
- Weights
- Bias

---

```java
class Neuron {
    double value;
    List<Weight> weights;
}

class Weight {
    double value;
    Neuron neuron;
}
```

---

### Neural network

![mnist](mnist.png "mnist")
![seven](seven.png "seven")

Note:
- 28 * 28 pixels
- Waarde van 0.0 - 1.0
- Dit is input layer voor ons neurale netwerk

---

### Neural network

![our_nn](our_nn.png "our_nn")

Note:
- 2 hidden layers
- voorbeeld komt van 3Blue1Brown

---

### Neural network

![artificial-neuron](artificial-neuron.png "artificial-neuron")

Note:
- 2 hidden layers
- voorbeeld komt van 3Blue1Brown

---

### Activation Function

`$$ \sigma(x) = \frac{1}{1 + e^{-x}} $$`<!-- .element: class="fragment fade-in" -->
`$$ ReLu(x) = max(0, x) $$`<!-- .element: class="fragment fade-in" -->
![activation](activation.png "activation")<!-- .element: class="fragment fade-in" -->

---

<!-- .slide: class="two-floating-elements" -->
###  Neuron

<img src="our_nn_small.png" width="40%">

* `$$(w_1 a_1 + w_2 a_2 + ... +w_n a_n)$$` <!-- .element: class="fragment fade-in-then-semi-out" -->
* `$$\sigma(w_1 a_1 + w_2 a_2 + ... +w_n a_n )$$` <!-- .element: class="fragment fade-in" -->
* `$$\sigma(w_1 a_1 + w_2 a_2 + ... +w_n a_n + \theta )$$` <!-- .element: class="fragment fade-in-then-semi-out" -->

---

### Neural network

`$$\sigma(w_{(1,1)} a_1 + w_{(1,2)} a_2 + ... +w_{1,n} a_n + \theta )$$`  <!-- .element: class="fragment fade-in-then-semi-out" -->
`$$
\sigma(
\begin{bmatrix}
w_{(1,1)} & w_{(1,2)} & \dots & w_{1,n} \\
\end{bmatrix}
\begin{bmatrix}
a_{1} \\
a_{2} \\
\vdots \\
a_{n}
\end{bmatrix}
+
\theta
)
$$` <!-- .element: class="fragment fade-in-then-semi-out" -->


`$$
\sigma
\left(
\left[
\begin{array}{ccc}
w_{(1,1)} & w_{(1,2)} & ... & w_{(1,n)} \\
w_{(2,1)} & w_{(2,2)} & ... & w_{(2,n)} \\
\vdots & \vdots  & \ddots & \vdots \\
w_{(m,1)} & w_{(m,2)} & ... & w_{(m,n)} \\
\end{array}
\right]
\begin{bmatrix}
a_{1} \\
a_{2} \\
\vdots \\
a_{n}
\end{bmatrix}
+
\begin{bmatrix}
\theta_{1} \\
\theta_{2} \\
\vdots \\
\theta_{n}
\end{bmatrix}
\right)
$$` <!-- .element: class="fragment fade-in-then-semi-out" -->

----

### Let's start!

- Initialize all values at random!

---

### But... it does not work! 

- We need it to improve <!-- .element: class="fragment" -->
- We need to quantify it's performance  <!-- .element: class="fragment" -->
- Define a "Cost function" <!-- .element: class="fragment" -->

Note:
- Met een Cost function kunnen we zeggen hoe slecht het werkt 

---

### Cost function of our Neural network

<!-- .slide: class="two-floating-elements" -->
![seven](seven.png "seven")
`$
\begin{bmatrix}
0.25_0 \\
0.81_1 \\
0.91_2 \\
0.52_3 \\
0.19_4 \\
0.76_5 \\
0.01_6 \\
0.25_7 \\
0.19_8 \\
0.44_9 \\
\end{bmatrix}
$`<!-- .element: class="fragment" -->

Note:

- Stel we hebben input voor ons neurale netwerk, Laten we zeggen een plaatje van het getal `7`.
- Wanneer we dit door ons neural netwerk sturen, komt hier onzin uit.

---

`$
\begin{rcases}
(0.25 - 0.00)^2 = 0.06 \\
(0.81 - 0.00)^2 = 0.65 \\
(0.91 - 0.00)^2 = 0.82 \\
(0.52 - 0.00)^2 = 0.27 \\
(0.19 - 0.00)^2 = 0.03 \\
(0.76 - 0.00)^2 = 0.57 \\
(0.01 - 0.00)^2 = 0.00 \\
(0.25 - 1.00)^2 = 0.56 \\
(0.19 - 0.00)^2 = 0.03 \\
(0.44 - 0.00)^2 = 0.19
\end{rcases} 3.18
$`

---

`$Cost(\underbrace{w_{(0,1)},w_{(0,2)} ... \theta_0, \theta_1}_{\text{Weights and biasses}})$` <!-- .element: class="fragment fade-in-then-semi-out" -->

`$Cost(w)$` <!-- .element: class="fragment fade-in-then-semi-out" -->

`$ Cost (w) = 0 \implies Cost^{-1}(0) = w $` <!-- .element: class="fragment fade-in-then-semi-out" -->

Note:
- We kunnen dit zien als een functie over alle parameters.
- Simpeler, maar hoe gaan we bepalen wat er moet veranderen?
- We willen weten wat de laagst mogelijke waarde is, calculus zou ons kunnen helpen?

---

- Stel dat de function eenvoudig zou zijn: `$f(x) = x^2$` 
- ![fx2](function/fx2.gif "fx2") <!-- .element: class="fragment" -->
- `$f'(x) = 0 \implies \frac {\delta} {\delta x} x^2 = 0 \implies  2x=0 \implies 0$` <!-- .element: class="fragment" -->

---

Complexiteit neemt snel toe:

`$ f(x) = x^5 - 5x^3 + 4x $` 
- ![fx2](function/hard.gif "fx2") <!-- .element: class="fragment" -->
- Wordt al moeilijker... <!-- .element: class="fragment" -->
- <span> Een onbekende (`$x$`)... </span> <!-- .element: class="fragment" -->

Note:
- met 1 input en 1 output zou dit kunnen
- niet met 13000 inputs, erg moeilijk om het te vinden, maar we kunnen het wel benaderen
- dit noemen we "Gradient descent"
- Multivariabele calculus

---

### Gradient descent

> Er is een methode `f` die berekend hoe stijl, en wat de richting is van de "Steepest Descent".  
<!-- .element: class="fragment" -->

<ol>
<li>bereken $ \nabla C $ </li><!-- .element: class="fragment" -->
<li>stap in $-\nabla C $ richting</li><!-- .element: class="fragment" -->
<li><code>goto 1</code></li><!-- .element: class="fragment" -->
</ol><!-- .element: class="fragment" -->

Hetzelfde werkt voor veel inputs  <!-- .element: class="fragment" -->

---
<!-- .slide: class="two-floating-elements" -->
Verzamel alle parameters in een vector

`$
\overrightarrow{W} =
\begin{bmatrix}
-0.35 \\
0.81 \\
-.41 \\
\vdots \\
0.57 \\
-0.94 \\
0.41 \\
\end{bmatrix}
$`<!-- .element: class="fragment" -->
`$
-\nabla C(\overrightarrow{W}) =
\begin{bmatrix}
0.15 \\
-0.41 \\
-.24 \\
\vdots \\
-.91 \\
0.14 \\
-0.82 \\
\end{bmatrix}
= \overrightarrow{W}_{next}
$` <!-- .element: class="fragment" --> <br><br><br><br>
`$\overrightarrow{W} = \overrightarrow{W} + \overrightarrow{W}_{next}$` <!-- .element: class="fragment" -->

----

### In practice

- Batching  <!-- .element: class="fragment" -->
- Stochastic Gradient Descent  <!-- .element: class="fragment" -->

---

# MNIST Example