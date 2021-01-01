---
title: Naive Bayes Algorithm
date: "2020-12-17"
template: "post"
draft: false
slug: "naive-bayes-algorithm"
category: "Machine Learning"
tags:
  - "Machine Learning"
  - "Probability"
  - "Classification"
description: "Exploring Naive Bayes: Mathematics, How it works, Pros & Cons, and Applications"
socialImage: "/media/naive/Imgs/img1.jpg"
---

### Exploring Naive Bayes: Mathematics, How it works, Pros & Cons, and Applications

![img2](/media/naive/Imgs/img1.png)

## What is Naïve Bayes Algorithm?
Naive Bayes is a classification technique that is based on Bayes’ Theorem with an assumption that all the features that predicts the target value are independent of each other. It calculates the probability of each class and then pick the one with the highest probability. It has been successfully used for many purposes, but it works particularly well with natural language processing (NLP) problems.
</br></br>
Bayes’ Theorem describes the probability of an event, based on a prior knowledge of conditions that might be related to that event.
</br></br>

## What makes Naive Bayes a “Naive” algorithm?
Naive Bayes classifier assumes that the features we use to predict the target are independent and do not affect each other. While in real-life data, features depend on each other in determining the target, but this is ignored by the Naive Bayes classifier.
</br></br>
Though the independence assumption is never correct in real-world data, but often works well in practice. so that it is called “Naive”.

## Math behind Naive Bays Algorithm
Given a features vector X=(x1,x2,…,xn) and a class variable y, Bayes Theorem states that:
</br></br>
![img2](/media/naive/Imgs/img2.png)

</br>
We’re interested in calculating the posterior probability P(y | X) 
</br></br>
from the likelihood P(X | y) and prior probabilities P(y),P(X).
Using the chain rule, the likelihood P(X ∣ y) can be decomposed as:
</br></br>
![img4](/media/naive/Imgs/img3.png)

but because of the Naive’s conditional independence assumption, the conditional probabilities are independent of each other.
</br></br>
![img4](/media/naive/Imgs/img4.png)

</br></br>
Thus, by conditional independence, we have:
</br></br>
![img5](/media/naive/Imgs/img5.png)

</br></br>
And as denominator remains constant for all values, the posterior probability can then be:
</br></br>
![img6](/media/naive/Imgs/img6.png)

</br></br>
The Naive Bayes classifier combines this model with a decision rule. One common rule is to pick the hypothesis that’s most probable; this is known as the maximum a posteriori or MAP decision rule.
</br></br>
![img7](/media/naive/Imgs/img7.png)

## How Naive Bays really works:
Let’s explain it using an example to make things clear:
</br>
Assume we have a bunch of emails that we want to classify as spam or not spam.
</br></br>
Our dataset has 15 Not Spam emails and 10 Spam emails. Some analysis had been done, and the frequency of each word had been recorded as shown below:
</br></br>
![img8](/media/naive/Imgs/img8.png)

</br></br>
**Note:** _Stop Words like “the”, “a”, “on”, “is”, “all” had been removed as they do not carry important meaning and are usually removed from texts. The same thing applies to numbers and punctuations._

## exploring some probabilities:##
- P(Dear|Not Spam) = 8/34
- P(Visit|Not Spam) = 2/34
- P(Dear|Spam) = 3/47
- P(Visit|Spam) = 6/47
</br>
and so on.
</br></br>
now assume we have the message _“Hello friend”_ and we want to know whether it is a spam or not.
</br>
so, using Bayes’ Theorem
</br></br>
![img9](/media/naive/Imgs/img9.png)
</br>
ignoring the denominator
</br></br>
![img10](/media/naive/Imgs/img10.png)

</br>
But, P(Hello friend | Not Spam) = 0, as this case (Hello friend) doesn’t exist in our dataset, i.e. we deal with single words, not the whole sentence, and the same for P(Hello friend | Spam) will be zero as well, which in turn will make both probabilities of being a spam and not spam both are zero, which has no meaning!!
</br></br>
But wait!! we said that the Naive Bayes assumes that `the features we use to predict the target are independent`.
so,
</br></br>
![img11](/media/naive/Imgs/img11.png)

</br>
now let’s calculate the probability of being spam using the same procedure:
</br></br>
![img12](/media/naive/Imgs/img12.png)

</br>
so, the message “Hello friend” is not a spam.

</br></br>
**now, let’s try another example:**
</br>
assume the message _“dear visit dinner money money money”_. It’s obvious that it’s a spam, but let’s see what Naive Bayes will say.
</br></br>
![img13](/media/naive/Imgs/img13.png)
![img14](/media/naive/Imgs/img14.png)
</br>

oops!! Naive Bays says that this message is not a spam?!!!
</br></br>
This happened because the word _“dinner”_ does not appear in the spam dataset, so that P(dinner | spam) = 0, hence all other probabilities will have no effect.
This is called the **Zero-Frequency Problem.** And to solve that we can use Laplace smoothing.

</br>
`**Laplace Smoothing** is a technique for smoothing categorical data. A small-sample correction, or pseudo-count, will be incorporated in every probability estimate. Hence, no probability will be zero. this is a way of regularizing Naive Bayes.
</br></br>
Given an observation x = (x1, …, xd) from a multinomial distribution with N trials and parameter vector θ = (θ1, …, θd), a “smoothed” version of the data gives the estimator:`

</br>
![img15](/media/naive/Imgs/img15.png)
</br>
`where the pseudo-count α > 0 is the smoothing parameter (α = 0 corresponds to no smoothing).
ead more about **Additive Smoothing** <a href='https://en.wikipedia.org/wiki/Additive_smoothing'>here</a>`

</br></br>

Back to our problem, we are going to pick α = 1, and ‘d’ is the number of the unique words in the dataset which is 10 in our case.
</br></br>
![img16](/media/naive/Imgs/img16.png)
![img17](/media/naive/Imgs/img17.png)
![img18](/media/naive/Imgs/img18.png)

</br></br>
Now it’s correctly classified the message as spam.
</br>

## Types of Naive Bayes Classifiers
- **Multinomial:** Feature vectors represent the frequencies with which certain events have been generated by a multinomial distribution. For example, the count how often each word occurs in the document. This is the event model typically used for document classification.
- **Bernoulli:** Like the multinomial model, this model is popular for document classification tasks, where binary term occurrence(i.e. a word occurs in a document or not) features are used rather than term frequencies(i.e. frequency of a word in the document).
- **Gaussian:** It is used in classification and it assumes that features follow a normal distribution.

## Pros and Cons for Naive Bayes
- **Pros:**
  - Requires a small amount of training data. So the training takes less time.
  - Handles continuous and discrete data, and it is not sensitive to irrelevant features.
  - Very simple, fast, and easy to implement.
  - Can be used for both binary and multi-class classification problems.
  - Highly scalable as it scales linearly with the number of predictor features and data points.
  - When the Naive Bayes conditional independence assumption holds true, it it will converge quicker than discriminative models like logistic regression.
- **Cons:**
  - The assumption of independent predictors/features. Naive Bayes implicitly assumes that all the attributes are mutually independent which is almost impossible to find in rea-world data.
  - If a categorical variable has a value that appears in the test dataset, and observed in the training dataset, then the model will assign it a zero probability and will not be able to make a prediction. This is what we called the “Zero Frequency problem“, and can be solved using smoothing techniques.

## Applications of Naive Bayes Algorithm
- Real time Prediction.
- Multi-class Prediction.
- Text classification/ Spam Filtering/ Sentiment Analysis.
- Recommendation Systems.
