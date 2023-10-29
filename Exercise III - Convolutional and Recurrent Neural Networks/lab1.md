# The report!

## Joel Bengs

## Introduction
In this lab, the training of Artifical Neural Networks (ANN) is investigated with focus on the three parameters _learning rate, minibatch size and epochs_.
## Answers to questions
Provide enough information to clarify the meaning of your answers, so that they can be understood by someone who does not scroll up and read the entire instruction.

The questions are repeated here, for clarity of what is demanded. If it does not fit your style to quote them verbatim, change the format.

#### Question 1, variations in pre-defined MLP
(a) Do you see the same loss vs epoch behavior each time your run? If not, why?

No, the behaviour is different on each iteration:
1. The initial loss is random as the inital weights are random. On the first epoch, there is a substantial improvement
2. After 4000 epochs, the end result can vary widely (best/worst: 0.004/0.4). Only one of five runs had a succesful output (loss < 0.01).
3. The optimization method is always improving with more epochs, but at different rates. This is because the optimization walk sometimes has to work in an envorinment where only small improvements are possible (flat areas or stuck around a local minimum). The stocastic gradient descent method is designed to mitigate these issues (hence the process never gets completely stuck but always improves with more epochs), but after a set number of epochs the optimization will have reached different results.

(b) Do you observe that training fails, i.e. do not reach low loss, during any of these five runs?

Yes, in four of five runs the loss reaches o.4, which is less than 0.01 and thus not "successful".

#### Question 2, vary learning rate
The result of varying learning rates are presented below. In each case, three networks with random initial weights were trained with graditent descent optimization and 4000 epochs, using an automated script.

Increasing the learning rate improved the result in general, up until a point. A larger learning rate means taking larger steps in the negative gradient direction. In the test, we have a set limit of steps. Thus the alogorithm can reach further within the set amount of steps if each step is larger. With larger steps come an increased risk of stepping to far, thus worsening the outcome. The lowest loss was achieved with a learning rate of 0.3. The learning rate 0.5 resultet in a diverging optimization walk.

Learning rate: 0.001

Average loss: 0.50736
___
Learning rate: 0.01

Average loss: 0.44835
___
Learning rate: 0.05

Average loss: 0.01200
___
Learning rate: 0.1

Average loss: 0.00184
___
Learning rate: 0.15

Average loss: 0.00117
___
Learning rate: 0.2

Average loss: 0.00085
___
Learning rate: 0.3

Average loss: 0.00040
___
Learning rate: 0.4

Average loss: 0.09827
___
Learning rate: 0.5

Average loss: nan
___
#### Question 3, vary (mini)batch size
In this exercise, six different batch sizes were tested: [50, 25, 13, 10, 8, 7]. Note that the data set is of size 50. For each batch size, three ANNs were trained with learning rate 0.05 and 4000 epochs. In this scenario, the ANN is deemed successful if it achieves a loss of less than 0.01, otherwize unsuccessful. The success of each run is presented below, and if the run was a success it is noted how many epochs were required to reach the threashold loss of 0.01. If the threshold was not reached in 4000 epochs, minus one is displayed.

There are patterns to be noted, but the results are too inconsistent and data points to few draw certain conculusions. It seems that a smaller batch size increases the ratio of success, and that the ANN can reach the threshold level faster (fewer epochs) with a smaller batch size. At the same time, the randomness in starting weights seem to be of high influence because the batch size 50 has one sucessful run while the batch size 8 has one unsuccessful run.


Batch size:  50

Success of runs:  [False False  True]

Epoches until success [-1, -1, 2852]
___
Batch size:  25

Success of runs:  [ True  True False]

Epoches until success [1390, 715, -1]

___
Batch size:  13

Success of runs:  [ True False  True]

Epoches until success [1591, -1, 2014]
___
Batch size:  10

Success of runs:  [ True  True  True]

Epoches until success [787, 1782, 1380]
___
Batch size:  8

Success of runs:  [False  True  True]

Epoches until success [-1, 414, 1443]
___
Batch size:  7

Success of runs:  [ True  True  True]

Epoches until success [1302, 791, 208]
___

#### Question 4, select good hyper-parameters
_Present your best combination of learning rate and batch size, and its result._

An automated script was written, that evaluated all 16 combinations of the batch sizes [25,13,10,7] and the learning rates [0.05, 0.1, 0.2, 0.3]. For each scenario, five ANN networks were trained using 1000 epochs. Each network achieved some final loss, heavily dependent on the randomness of the inital weights, and so the avarages of these final losses were calculated and are presented below, with arrws indicating the minimal values. Epoches to success is an avarage of the numebrs of epoches needed to reach loss 0.01, only taking into account the successful runs. A network that never achieved success therefore has -1 as epoches to success.

The combination __batch size 10 and learning rate 0.2__ achieved the smallest avarage loss of 0.00171, closely followed by __batch size 13 and learning rate 0.3__. These were the only two that could achieve success in all five networks. The avarage number of epoches needed to reach success for these parameters were 478 and 595 respectively. The cobination __13/0.3__ will be used in Q5 as batch size 13 had a better general performance.

The batch size 13 had the lowest loss when avaraged over all learning rates, while the learning rate 0.1 had the lowest loss when avaraged over all batch sizes. It thus seems that different perspectives on the problem yield different results.

The ANNs that could not be successfuly trained ended with a loss much larger than 0.01, influencing the avarage disproportionally. Therefore the networks that had two or more failures had an avarage loss far greater than the success threashold of 0.01.

It should be noted that the randomness of inital weights had such large impact that the optimal parameters changed when the experiment was rerun.

Batch / rate / avarage loss / success rate / epoches to success

25 / 0.05 / 0.75571 / 0% / -1

25 / 0.1 / 0.16820 / 60% / 693

25 / 0.2 / 0.39073 / 40% / 634

25 / 0.3 / 0.72816 / 0% / -1

13 / 0.05 / 0.30835 / 40% / 744

13 / 0.1 / 0.19806 / 40% / 650

13 / 0.2 / 0.25686 / 60% / 816

__13 / 0.3 / 0.00178 / 100% / 478__ <---

10 / 0.05 / 0.54697 / 20% / 333

10 / 0.1 / 0.42347 / 20% / 273

__10 / 0.2 / 0.00171 / 100% / 595__ <---

10 / 0.3 / 0.82806 / 0% / -1

7 / 0.05 / 0.49050 / 0% / -1

7 / 0.1 / 0.22922 / 60% / 623

7 / 0.2 / 0.90141 / 0% / -1

7 / 0.3 / 0.93302 / 0% / -1


Avarage loss with batch size __25__:  0.51070

Avarage loss with batch size __13__:  0.19126 <---

Avarage loss with batch size __10__:  0.45005

Avarage loss with batch size __7__:  0.63854

Avarage loss with learning rate __0.05__:  0.52538

Avarage loss with learning rate __0.1__:  0.25474 <---

Avarage loss with learning rate __0.2__:  0.38768

Avarage loss with learning rate __0.3__:  0.62275


#### Question 5, vary epochs

When training a network on the more diffcult dataset _reg1_, the ANN could not converge to a loss less than 0.5 within 1k, 10k or even 50K epochs. Trying out different design parameters finaly yieled a convering network that could converge to a successful loss < 0.01 when allowed 50k epoches, using roughly 20k epoches to get there. The design was batch size 13 with learning rate 0.1, achieving the final loss 0.00023. Plots of the model are presented below. Looking back at Q4, this network had a 40% success rate, with 0.19 as an avarage loss and an avarage of 650 epoches to reach the threashold in the successful cases. The difference in epoches needed is factor 50 between the two problems!

It might be the case that the inital randomness played an important role, as each network was trained only once.

Model: Batch size 13, learning rate 0.1, epochs 50000
Result: MSE = 0.0002339039

![image.png](attachment:image.png)

![image-2.png](attachment:image-2.png)


#### Question 6, vary network size and other hyper-parameters
The network was trained with a larger network size on a larger data set wih 75 patterns. The hyper-parameters were kept the same as in Q5: Batch size 13, learning rate 0.1, epochs 50000. The network size was [10,5,5], that is three hidden layers of size 10, 5, 5.

Again, the ANN converged in rougly 20k epochs, with a final MSE of  0.0002056086. Plots are attached below.


![image-3.png](attachment:image-3.png)

![image-4.png](attachment:image-4.png)

#### Question 7, optimize hyper-parameters for classification
A new dataset was loaded, this time a classification problem with 100 patterns. To gain understanding of the problem at hand, a few networks with different combinations of parameters were trained without an automatic script. From the simple 2D-plot, it is clear that no single perceptron will be able to reach 95% accuracy. There are 100 patterns in the data set, hence the network may only missclasify 5 patterns. The best any linear descision boundary can do (given the data set generated with seed 10) is 11 missqualified patterns, giving 89% accuracy, as evident in the plot below:

_Plot: Linear descicion boundary after convergence to maximum accuracy possible with linearity_
![image-7.png](attachment:image-7.png)

The descicion boundary must be non-linear to achieve better accuracy, thus we investigate a more flexible network. Throughout Q7 and Q8, the randomness in inital weights was locked with seed 10. We are performing obvious overtraining when moving beyond a linear model in this case.

With a network with 2 or 3 hidden nodes, 95 % accuracy could not be reached in 10000 epoches, as presented below

![image-8.png](attachment:image-8.png)

![image-9.png](attachment:image-9.png)

A network with 3 hidden layers with 10, 5, and 5 nodes respectively could reach 98% accuracy when trained with a minibatch size of 10, a learning rate of 0.03 and 10K epochs. The highly irregular model is ploted below. The same model but with learning rate of 0.01 could reach 96% accuracy, and this model is plotted further below.

![image-5.png](attachment:image-5.png)

![image-6.png](attachment:image-6.png)


#### Question 8, change learning algorithm
Try the Adam optimizer for Q7, and compare (qualitatively) the results and the number of epochs needed to get them. Present changes you needed to make to improve the results of the Adam optimizer, if any.

The Stochastic Gradient Descent method was replaced with Adams optimization method to potentially achieve even higher accuracy. Five learning rates (0.001, 0.01, 0.03, 0.05, 0.1) were investigated on a simple network with two hidden nodes in one layer, trained with  a limited 1000 epochs. The purpose was to find a somewhat optimized learning rate for the Adams algorithm. 0.01 produced the best result, but it should be noted that this is not a general result.


With Adam, __learing rate 0.01, batch size 10 and 10K epochs, 96 % accuracy__ could be reached but the loss/epochs graph is fluctuating heavily. The descision boundary was also highly irregular, see below.
![image-10.png](attachment:image-10.png)

![image-11.png](attachment:image-11.png)

4 further networks were trained as per below. None could perform better than the above example. A shared attribute was that all had fluctuating loss/epoch-graphs. The descicion boundaries were highly irregular for all examples.

Network structure / learing rate / epochs / minibatch size / accuracy

[10,5,5] / 0.02 / 10K / 10 / __90%__

[10,5,5] / 0.01 / 10K / 25 / __91%__

[10,5,5] / 0.02 / 10K / 25 / __93%__

[10,5,5] / 0.01 / 30K / 10 / __93%__

In conclusion, The adams optimization method was less stable than the SGD and could not reach the same level of accuracy (overtraining) as SGD within this limited experiment.

#### Bonus tasks (if you feel inspired)

Not today, too much on the schedule. But this was a very fun lab, and I spent a lot of time to play around with Q1-Q4 just for the fun of it and to understand Python! Looking forward to the next lab.

## Summary
Connect the summary to your introduction, to provide a brief overview of your findings.
  
