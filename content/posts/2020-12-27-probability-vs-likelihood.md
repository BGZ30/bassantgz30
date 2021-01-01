---
title: Probability vs Likelihood
date: "2020-12-27"
template: "post"
draft: false
slug: "probability-vs-likelihood"
category: "Machine Learning"
tags:
  - "Likelihhod"
  - "Probability"
description: "Clear explanation for the difference between Probability and Likelihood with a practical example"
socialImage: "/media/probLikli/Imgs/cover.jpg"
---

### Clear explanation for the difference between Probability and Likelihood with a practical example
<p align="center">
          <img src="/media/probLikli/Imgs/cover.png">
</p>

</br>
In a dictionary, you may find that "probability" and "likelihood" are usually synonyms and sometimes are used interchangeably, but from statistics' point of view they implicitly refer to distinct things. Probability talks about the outcomes(data)/hypothesis, while likelihood talks about the model/evidence. In this article, we are going to show how probability is different from likelihood and also show some examples.
</br></br>

## Probability
Talks about the data/hypothesis. It refers to finding the chance that a particular event occurs given a distribution of the data or some conditions/evidence. Probability is the percentage that an event will occur, it talks about the future and it's written as **P(Hypothesis|Evidence).**
</br></br>
In probability function, the model parameters are known and the data/outcome has to be found. For example, in a binomial distribution, you know the number of trials and the probability of success in each trial, based on this, you can find the probability of occurrence of a particular event.

</br>

To make it more clear, assume you have a fair coin, so you know that the probability of success 'p' is 0.5, and you are going to flip it three times. Now you would like to know the probability that you will get (heads, heads, tails).

</br>

Assuming that success means heads and failure means tails, **P(H)=0.5**, and **P(T) = 1 - P(H) = 0.5**
</br>
Now, you would like to calculate **P(HHT|p=0.5).**
</br>
**Note:** here the hypothesis is 'HHT' and the evidence is (p=0.5).

## Likelihood
Talks about the model/evidence. In simple terms, we try to fit a distribution to data. It talks about the past as the event had been already happened. It can be written as **P(Evidence|Hypothesis).**
</br></br>
In a likelihood function, the data/outcome is known and the model parameters have to be found. For example, in a binomial distribution, you know the number of successes and fails and would like to know the probability of success.

</br>

To make it more clear, assume your friend told you that he/she flipped a coin three times and got (HTH), and asked you to guess whether it’s a fair coin or not.
Here you are trying to calculate **P(p=0.5|HTH).**
</br></br>
Here, the hypothesis is (p=0.5) and the evidence is ‘HTH’.
</br>
**Note:** you may also try different values for ‘p’ to find the best likelihood knowing that ‘p’ can take any value between 0 and 1.

</br>

Now let’s see a practical example to make things more clear.
</br></br>

<img align="right" src="/media/probLikli/Imgs/probability.png"> </br>
Assume you have a box that contains seven balls, four of them are red, and the other three are green. You picked three balls at random without replacement. **"Without replacemen"** means that once you picked a ball, you do not put it back in the box before selecting a new ball. Picking without replacement makes the draws dependent, since the color of each picked ball does affect the following draws.
</br></br>

Imagine that it was a game, and you win if you get red in the first draw, green in the second draw and red in the third draw. You would like to know the probability that you will get the right sequence and win the game.
</br></br>
So you are going to calculate P(RGR | R=4, G=3). </br>
1. Before making any draws, there are seven balls inside the box
    - P(red) = 4/7
    - P(green) = 3/7
    - **The probability that the first drawn ball is red = 4/7**  
2. Now there are six balls inside the box 
    - P(red) = 3/6
    - P(green) = 3/6
    - **The probability that the second ball is green = 3/6**  
3. Now there are five balls inside the box
    - P(red) = 3/5
    - P(green) = 2/5
    - The probability that the third ball is red = **3/5** 
4. Finally, **P(RGR| R=4, G=3) = (4/7) * (3/6) * (3/5) = 0.17**
</br>

Which means that there is a probability of __17%__ that you get the right sequence and win the game.
</br></br>
In the above example we know the conditions/model’s parameters which are the numbers of balls, and we calculated the probability of an outcome.
</br></br></br>
<img align="right" src="/media/probLikli/Imgs/liklihood.png">
Now assume again that we have a box with ten balls. The balls are red, green and blue, but we don’t know how many red, green or blue are there. We picked three balls at random without replacement, the first was green, the second was red, and the third was green.
</br></br>
Now we would like to know how many red, green and blue balls are there. Of course we can’t make a guess with 100% confidence, we can just make “likelihoods” about the model(box).
</br>


#### Some facts: </br>
- There are **66 different possible combinations** of red, green and blue balls that would add up to 10. *If you are interested to know how we got 66, look [here](https://math.stackexchange.com/a/1462106)*
- Not all of the 66 combinations are valid.
- There is at least one red ball as we already got a red ball.
- There are at least two green balls, since we got two green balls in our draws.
- P(GRG) = (G/10) * ( R/9) * ((G-1)/8)
</br></br>

To make calculations simple and clear, I am going to use a simple python code to help me calculate those likelihoods.
</br>
<img src="/media/probLikli/Imgs/code_1_balls.png"> </br></br>

*‘balls’* contains all the combinations of the numbers in sets of three which are 1331 different combinations (11\*11\*11), it looks like this: </br>
<img src="/media/probLikli/Imgs/all_combinations.png"> </br></br>

Now we should filter those combinations as they are not all valid. As you can see, there are some case in which the sum of the balls is not ten. </br>
<img src="/media/probLikli/Imgs/code_2_ten_only.png">  </br></br>

Now we got the following list:  </br>
<img src="/media/probLikli/Imgs/sum_to_10.png">   </br></br>

Again, not all those are valid, we know that there are at least one red ball and at least two green balls.  </br>
<img src="/media/probLikli/Imgs/code_3_valid_all.png">  </br></br>

Now the valid combinations are:  </br>
<img src="/media/probLikli/Imgs/valid_all.png">   </br></br>

Finally, calculate the probabilities of ‘GRG’ for each combination:  </br>
<img src="/media/probLikli/Imgs/code_4_liklihood_all.png">   </br></br>
The likelihoods are:  </br>
<img src="/media/probLikli/Imgs/liklihood_without_blue.png">  </br></br>

Now we have the likelihoods of the model. For example if the box has **2 red balls, 7 green balls and 1 blue ball, then there is a 11.67% probability that we get (GRG) when we pick three random balls.**
</br></br>

What we did so far, is we tried to force the model to fit our data. i.e. we forced the box to have at least one red ball and two green balls to guarantee that we have the chance to pick one red and two green balls.
</br></br>

Now if we want to go further and make the best predictions, we will chose the maximum likelihood to represent our model (box). </br>
<img src="/media/probLikli/Imgs/max_liklihood_without_blue.png"> </br></br>
This means that we are 17.5% sure that the box has three red balls, seven green balls, and no blue balls. Note that the maximum likelihood occurred when there are no blue balls in the box. 
</br>

But if we are sure that there is at least one blue ball in the box, then we should exclude the combinations in which there are no blue balls.
<img src="/media/probLikli/Imgs/code_5_with_blue.png"> </br></br>

Now the likelihoods are: </br>
<img src="/media/probLikli/Imgs/max_liklihood_with_blue.png"> </br></br>

And the maximum likelihood now is 12.5%.
</br></br>

### Maximum likelihood
Refers to finding the best values for model’s parameters given some outcomes/data.
</br>
This means to increase the chance of a particular event to occur by varying the characteristics/parameters of the data distribution/model.
</br></br>

### Summary
- Probability is a function of possible values of the data given the model parameters.
- Likelihood is a function of possible values of the model parameters given the data.
- Probability is used to find the chance of occurrence of a particular situation.
- Likelihood is used to generally maximize the chances of a particular situation to occur.
</br></br>
***
I hope this article helps you understand the difference between probability and likelihood. Please let me know if anything is unclear. In future articles we are going to discuss the maximum-likelihood for different kinds of distributions.
</br></br>

#### To learn more: </br>
- Check some awesome answers about probability vs likelihood [here](https://stats.stackexchange.com/questions/2641/what-is-the-difference-between-likelihood-and-probability).
- Check [this](https://qr.ae/pNcZOv) answer on Quora for a very nice example.
- More about likelihood function on Wikipedia [here](https://en.wikipedia.org/wiki/Likelihood_function).
- More about maximum-likelihood estimation [here](https://online.stat.psu.edu/stat504/node/28/).