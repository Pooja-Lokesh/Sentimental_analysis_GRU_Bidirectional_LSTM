# Sentimental analysis 

## Steps followed :
- Tokenize the text to generate numbers for the words. Optionally set the max number of words to tokenize. The out of vocabulary (OOV) token represents words that are not in the index.
- The numbers in the word index are not ordered, therefore, need to generate sequences for the sentences.
- Adjust the sequences to all be the same length, either by padding them with zeros and/or truncating them.

## Why embeddings ?
- Represent words as semantically-meaningful dense real-valued vectors.
- This overcomes many of the problems that simple one-hot vector encodings have.
- Most importantly, embeddings boost generalisation and performance for pretty much any NLP problem, especially if you don’t have a lot of training data.


## Simple RNN : 
- RNN have sequential memory.
- It adds a loop to neural netwrok which can pass information forward.
- This information is a hidden state which is a representation of previous inputs.
- it takes one word at a time, produces the output, then for the next round takes in the next word till it reaches the end of the sentence.
- Simple RNN has a problem with retaining the informtaion from the earlier layers 
- This happens because the nodes in a layer compute the gradient wrt the gradient in the layer before, so if the gradient in smaller before, then the gradient will be even more smaller in the present layer,the gradients decrease exponentially.
- Due to this the earlier layers barely learn anything, which leads to vanishing gradient problem. 
- Uses tanh cativation function which squishes values form -1 to 1.


## Why LSTMs and GRUs ?
- Due to vanishing gradient problem in simple RNNs, we need LSTMs and GRU. 
- They are capable of learning long term dependencies through gates.  
- These gates decide which information to add or remove from hidden state


## LSTM : 
- Cell state is the medium through which information flows in the network, it is a memory of a network.
- Gates decide to keep or forget a particular informationa as we progress sequentially in RNN
- This uses sigmoid activation function , it squishes values from 0 to 1
- The forget gate decides which informstion to pass on and which information to forget 
    * the input and the previous hidden state is passed to sigmoid function 
    * the closer to 0 means forget and closer to 1 means keep
the input gate 
    the hidden state and input is passed through the sigmoid 
    this decides whoch values need to be updated 
    0 means important 1 means not 
    pass the hidden state an dthe input through the tanh function
    the tan output and the sigmoid output are multiplied
    the sigmoid function decides which information to keep from the tan output
calcculating cell state :
    the cell state is multiplied by the forget vector 
    polarized addition is performed on the cell state and the input gate 
    this gives us new cell state 
output gate 
    this decides which should be the new hidden state 
    the previous hidden state and the input is passed to the sigmoid function 
    the new cell state is passed through the tanh function 
    the output from the sigmoid function and the tanh function are multiplied 
    new hidden state is generated 
these new cell and hidden states are passed to the next step 


## GRU :

update gate :
    The update gate helps the model to determine how much of the past information (from previous time steps)
    needs to be passed along to the future.
reset gate :
     It determines how much of the past knowledge to forget. 
less tensor operations 
