<h1 align = 'center'> Reading with Neural Networks
</h1>

<p align='center'>
  An effort has been made to determine the readability of the text with the help of Neural Netwroks. Readability, here implies the difficulty in reading the text. 
  This was done as a part of Kaggle competition "CommonlitReadaability"
</p>

## Concepts used
* **CNNs (Convolutional Neural Network)** - CNNs is a type of neural network which uses a convoltuional filter of given channels and sizes as the weights. CNNs is usually used on images as it can easily extract features of images.
* **RNNs (Recurrent Neural Networks)** - RNNs are a type of neural network which are primarily useful for sequential data. At the first time step, they take one input, process it, and then this output also called 'hidden state' is used in the next time step along with the new input. There is only one cell i.e. the weights of the same RNN cell are updated at each time step. 
* **LSTMs (Long Short Term Memory)** - LSTM is a type of RNN which instead of only one hidden state use two hidden states, one for the long term memory and the other for the short term memory.
* **Attention** - In attention mechanism, ouputs of the encoder are given a weight and then fed to the decoder. The attention pretty much says how much attention one needs to give to that particular output.

## Approaches Used 
In order to estimate the readability score of the passage in question, different types of architectures have been tried out. 
One thing to note that is only the RNN based architectures are used in this project. All the models tried out are without using Transformer architectures.

* The very first thought when we work with textual data is the RNN architecture. So, initially, the model is tried out using only RNN architecture. 
* Next Attention is added to the RNN arhcitecture. This improves the result marginally. 
* Now, LSTM is used. Then LSTM with attention. There are minute variations in the reuslts.
* To pull up the game, CNN layer is added after the embedding layer. This is used as a filter in order to pass the weightso of the proximity factor to the RNN layer.
* Next, CNN is tried out at the output of the RNN. Three different CNNs with different kernel sizes are used in order to get the local, medium local and far-away context of the embeddings of the RNN output.
* CNN-LSTM-CNN is tried. This doesn't give much improvement over LSTM-CNN
* These versions are also tried out with the Attention mechanism. This does improve the performance significantly. 

### Ensemble Model 
We try to make significant changes to the architecture in the Ensemble model. In this, we make two blocks- Block 1 and Block 2. The embeddings are passed through both the blocks and the output of both the blocks are then combined
<ul>
<li>Block 1 - In the block 1, there is an lstm followed by attention and then the global context is passed through another LSTM layer. 
<li>Block 2 - In the block 2, there is an LSTM later followed by three CNN layers. The three CNN layer have differnet kernel size providing the local, medium and long-term context. These three are then passed through three different LSTM layers and then their outputs are concatenated. 
</ul> 
The outputs of Block 1 and Block 2 are combined with linear layers. 
