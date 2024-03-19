# Ⅰ -- Math Assignment:
## Raw Forward Propagation

1. **Input to Hidden Layer Computation:**
   - For each neuron in the hidden layer, the input is the dot product of the $\( x \)$ vector and the weights $\( w \)$, since there is no bias term, so $\( out = x \cdot w \)$.
   - Given that the initial weights are 0.1, we have three inputs $\( x = [6, 2, 2] \)$.
   - Therefore, the $\( out \)$ for each neuron in the hidden layer will be $\( 6 \times 0.1 + 2 \times 0.1 + 2 \times 0.1 = 1.0 \)$.

2. **Activation in Hidden Layer:**
   - Apply the ReLU activation function, $\( \text{ReLU}(out) = \max(0, out) \)$, since $\( out \)$ is 1.0, the output after activation remains $1.0$.

3. **Hidden to Output Layer Computation:**
   - Similarly, the $\( out \)$ for the output layer is also the dot product of the inputs, $\( out = 1.0 \times 0.1 + 1.0 \times 0.1 = 0.2 \)$.

4. **Activation in Output Layer:**
   - Apply the ReLU activation function to the output layer, $\( \text{ReLU}(out) = \max(0, 0.2) = 0.2 \)$.
   - So, the raw modeled output $\( \hat{y} \)$ is $0.2$.

## Backpropagation

To compute the gradient and update the weights, we use the loss function $\( L = y - \hat{y} \)$ and a learning rate of 0.05.

1. **Loss Computation:**
   - The given true value $\( y = 0.7 \)$, the model output $\( \hat{y} = 0.2 \)$.
   - The loss $\( L = y - \hat{y} = 0.7 - 0.2 = 0.5 \)$.

2. **Gradient for Output Layer Weights:**
   - $\( \frac{\partial L}{\partial w} = \frac{\partial L}{\partial \hat{y}} \cdot \frac{\partial \hat{y}}{\partial w} \)$.
   - $\( \frac{\partial L}{\partial \hat{y}} = -1 \)$ since the loss function is $\( L = y - \hat{y} \)$.
   - $\( \frac{\partial \hat{y}}{\partial w} \)$ is the derivative of the ReLU function times the output of the hidden layer. Since ReLU's derivative is a unit step function, for $\( out = 0.2 \)$, it is $1$.
   - The output of the hidden layer is 1, so $\( \frac{\partial \hat{y}}{\partial w} = 1 \)$.
   - Thus, the gradient for the output layer weights $\( \frac{\partial L}{\partial w} = -1 \times 1 \times 1 = -1 \).$

3. **Gradient Calculation for Hidden Layer Weights:**
   - The gradient for hidden layer weights (since only one hidden layer neuron outputs a positive value, hence its gradient is non-zero):
     $\( \frac{\partial L}{\partial w_{\text{hidden}}} = \frac{\partial L}{\partial \hat{y}} \cdot \frac{\partial \hat{y}}{\partial \text{out}_{\text{hidden}}} \cdot \frac{\partial \text{out}_{\text{hidden}}}{\partial w_{\text{hidden}}} \)$
   - As $\( \text{out}_{\text{hidden}} \)$ is activated by ReLU, its derivative is 1 for $\( \text{out} > 0 \)$, hence:
     $\( \frac{\partial \hat{y}}{\partial \text{out}_{\text{hidden}}} = w_{\text{out}} = 0.1 \)$
   - $\( \frac{\partial \text{out}_{\text{hidden}}}{\partial w_{\text{hidden}}} \)$ is the input $\( x \)$, hence:
     $\( \frac{\partial L}{\partial w_{\text{hidden}}} = -1 \times 0.1 \times x = -1 \times 0.1 \times [6, 2, 2] = [-0.6, -0.2, -0.2] \)$

4. **Update Weights:**
   - After computing gradients for all weights, update them simultaneously:
   - For the output layer weights $\( w_{\text{out}} \)$:
     $\( w_{\text{out}_{\text{new}}} = w_{\text{out}_{\text{old}}} - \alpha \times \frac{\partial L}{\partial w_{\text{out}}} = 0.1 - 0.05 \times -1 = 0.1 + 0.05 = 0.15 \)$
   - For the hidden layer weights $\( w_{\text{hidden}} \)$, for each corresponding input $\( x_i \)$:
     $\( w_{\text{hidden}_{\text{new}_6}} = w_{\text{hidden}_{\text{old}_6}} - \alpha \times \frac{\partial L}{\partial w_{\text{hidden}_6}} = 0.1 - 0.05 \times -0.6 = 0.1 + 0.03 = 0.13 \)$
     $\( w_{\text{hidden}_{\text{new}_2}}= w_{\text{hidden}_{\text{old}_2}} - \alpha \times \frac{\partial L}{\partial w_{\text{hidden}_2}} = 0.1 - 0.05 \times -0.2 = 0.1 + 0.01 = 0.11 \)$
## Updated Forward Propagation

1. **Input to Hidden Layer Computation:**
   - For each neuron in the hidden layer, the input is the dot product of the $\( x \)$ vector and the updated weights $\( w_{\text{new}} \)$, since there is no bias term, so $\( out = x \cdot w_{\text{new}} \)$.
   - Given that the initial weights are 0.1, we have three inputs $\( x = [6, 2, 2] \)$.
   - Therefore, the $\( out \)$ for each neuron in the hidden layer will be $\( 6 \times 0.13 + 2 \times 0.11 + 2 \times 0.11 = 1.22 \)$.

2. **Activation in Hidden Layer:**
   - Apply the ReLU activation function, $\( \text{ReLU}(out) = \max(0, out) \)$, since $\( out \)$ is 1.22, the output after activation remains $1.22$.

3. **Hidden to Output Layer Computation:**
   - Similarly, the $\( out \)$ for the output layer is also the dot product of the inputs, $\( out = 1.22 \times 0.15 + 1.22 \times 0.15 = 0.366 \)$.

4. **Activation in Output Layer:**
   - Apply the ReLU activation function to the output layer, $\( \text{ReLU}(out) = \max(0, 0.366) = 0.366 \)$.
   - So, the updated modeled output $\( \hat{y}_{\text{new}} \)$ is $0.366$.
## The Final Answer is [0.366]()
