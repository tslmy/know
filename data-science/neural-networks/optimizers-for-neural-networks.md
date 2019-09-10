---
description: Various Gradient Descent optimizers.
---

# Optimizers For Neural Networks



![](../../.gitbook/assets/image%20%2811%29.png)

## Optimizers For Neural Networks

### **Gradient Descent**: Take steps proportional to the negative of the gradient of the loss function \(i.e. error surface\) at the current point.

![](assets/52D0F4B0-53ED-425D-A7A4-DDD8B068B3C3.png)

[http://ruder.io/optimizing-gradient-descent/](https://arxiv.org/pdf/1609.04747.pdf)

[hackernoon.com](https://www.google.com/imgres?imgurl=https://cdn-images-1.medium.com/max/1600/1*f9a162GhpMbiTVTAua_lLQ.png&imgrefurl=https://hackernoon.com/gradient-descent-aynk-7cbe95a778da&h=768&w=1366&tbnid=Yiarh4BgHGVUpM:&q=gradient+descent&tbnh=118&tbnw=211&usg=__VfMGRoPiSiuJ5eBqfdc35ljYQok%3D&vet=1&docid=WPS3uPTi7A72oM&sa=X&ved=0ahUKEwiz-fjY1oPcAhWptVkKHS9gC0cQ9QEILTAA)  
**Gradient descent** is a first-order iterative optimization algorithm for finding the minimum of a function. To find a local minimum of a function using **gradient descent**, one takes steps proportional to the negative of the **gradient** \(or approximate **gradient**\) of the function at the current point.  
[Gradient descent - Wikipedia](https://en.wikipedia.org/wiki/Gradient_descent)  
[https://en.wikipedia.org/wiki/Gradient\_descent](https://en.wikipedia.org/wiki/Gradient_descent)

#### _tricks by modifying the training examples taken into consideration_

* \(**Standard/Full-Batch\) Gradient Descent**: Compute gradient w.r.t. ALL training examples. Update with this single gradient for once. ![](assets/A18849D1-A8D8-4549-AF31-AE2E4BD0C4BC.png)
* **Mini Batch Gradient Descent / SGD with Mini-Batch**: Compute a gradient w.r.t. EVERY so many training examples w/o replacement. Update parameters as soon as each gradient is computed.
* **Stochastic Gradient Descent \(SGD**\): Compute a gradient w.r.t. EACH training example. Update parameters as soon as each gradient is computed. ![](assets/03AC4BF3-6095-42C9-AE74-C1D58A0BAE65.png)

#### _tricks by considering previous values of the vector_

* **SGD w/ Momentum**: Update the vector with the gradient, then add a fraction of the previous values of the vector \(the “momentum”\) to the current vector. \(Essentially a “decaying average”.\) ![](assets/197E8E1C-834B-4F9A-A59C-A21DF5D9FCD5.png)
  * **Nesterov's Accelerated Descent**: Update the vector with the momentum first, THEN compute and update with the gradient. 
* **Averaged SGD**: Keeps track of all values taken by the vector. After training, replace the vector with the average of these historical values.

#### _tricks by modifying the learning rate_

* “**LRV - Learning Rate as Vectors**”: Replaces the General Learning Rate with a vector. \(i.e. Each parameter has its own learning rate now.\)
* **Adaptive Learning Rates**: \(with LRV\) At each step, for each LR in the LR Vector, update it to be the General LR divided by something.
  * **AdaGrad \(Adaptive Gradient**\): Divided by the root of the sum of the square of all previous gradients’ values. ![](assets/08F6CBE1-1825-40CE-9923-5CA24188EF94.png)
  * **RMSProp**: Divided by the root of a moving average of the square of a fixed window \(of size _t_\) of previous gradients’ values. ![](assets/6622278B-EFA6-4B3A-B9A0-6CA4BB9A30EC.png) [http://www.cs.toronto.edu/~tijmen/csc321/slides/lecture\_slides\_lec6.pdf](http://www.cs.toronto.edu/~tijmen/csc321/slides/lecture_slides_lec6.pdf)
  * **AdaDelta** ![](assets/3F5D53E2-6D28-442C-BAFE-54004A63A01B.png) [https://arxiv.org/pdf/1212.5701v1.pdf](https://arxiv.org/pdf/1212.5701v1.pdf)
    * _Idea 1_: Similar to RMSProp, but using a decaying average instead \(shown as root mean squared \(RMS\) error criterion of the gradient\).
    * _Idea 2_ \(THE “**AdaDelta**”\): Idea 1 + replace the GLR with also a decaying average of the last _t-1_ deltas in parameters’ historical values, for dimension \(“unit”\) correction.

#### _tricks by modifying the gradient itself_

[https://arxiv.org/pdf/1412.6980.pdf](https://arxiv.org/pdf/1412.6980.pdf)

* **AdaM \(Adaptive Moment Estimation**\): RMSProp + replacing the gradient w/ a decaying average of the gradient itself \(“momentum”\), for AdaGrad-like enhancement. \(\hat indicates bias-correction.\) ![](assets/B16803C3-C659-444D-8089-E9D3DD3404BD.png)
* **AdaMax**: AdaM + replacing the denominator \(i.e. root of a moving average of gradients\) with the higher value between \(biased\) last moving average of gradients and the magnitude of current gradient, for better stability. ![](assets/6E89FEC6-F041-446A-8CB5-82CED86D9D6B.png)
* **Nadam \(Nesterov-accelerated Adaptive Moment Estimation**\): Like AdaM, but momentum works in a Nesterov \(“momentum-then-gradient”\) manner.
* **AMSGrad**: Like AdaM, but uses the maximum previous value instead of the \(exponentially\) decaying average, for better convergence.
* **AdamW**
* **AdamWR**

