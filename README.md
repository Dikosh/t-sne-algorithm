# t-sne-algorithm
Step 2

For the low-dimensional counterparts  and  of the high-dimensional datapoints  and   it is possible to compute a similar conditional probability, which we denote by .



Note that, pi|i and pj|j are set to zero as we only want to model pair wise similarity.

In simple terms step 1 and step2 calculate the conditional probability of similarity between a pair of points in

High dimensional space
In low dimensional space
 For the sake of simplicity, try to understand this in detail. 

Let us map 3D space to 2D space. What step1 and step2 are doing is calculating the probability of similarity of points in 3D space and calculating the probability of similarity of points in the corresponding 2D space.  

Logically, the conditional probabilities  and must be equal for a perfect representation of the similarity of the datapoints in the different dimensional spaces, i.e the difference between  and  must be zero for the perfect replication of the plot in high and low dimensions.

By this logic SNE attempts to minimize this difference of conditional probability.

 

Step 3

Now here is the difference between the SNE and t-SNE algorithms. 

To measure the minimization of sum of difference of conditional probability SNE minimizes the sum of Kullback-Leibler divergences overall data points using a gradient descent method. We must know that KL divergences are asymmetric in nature.

In other words, the SNE cost function focuses on retaining the local structure of the data in the map (for reasonable values of the variance of the Gaussian in the high-dimensional space,).

Additionally, it is very difficult (computationally inefficient) to optimize this cost function.

So t-SNE also tries to minimize the sum of the difference in conditional probabilities. But it does that by using the symmetric version of the SNE cost function, with simple gradients. Also, t-SNE employs a heavy-tailed distribution in the low-dimensional space to alleviate both the crowding problem (the area of the two-dimensional map that is available to accommodate moderately distant data points will not be nearly large enough compared with the area available to accommodate nearby data points)  and the optimization problems of SNE.

 

Step 4

If we see the equation to calculate the conditional probability, we have left out the variance from the discussion as of now. The remaining parameter to be selected is the variance of the student’s t-distribution that is centered over each high-dimensional datapoint . It is not likely that there is a single value of that is optimal for all data points in the data set because the density of the data is likely to vary. In dense regions, a smaller value of  is usually more appropriate than in sparser regions. Any particular value of induces a probability distribution,  , over all of the other data points. This distribution has an 

This distribution has an entropy which increases as increases. t-SNE performs a binary search for the value of  that produces a  with a fixed perplexity that is specified by  the user. The perplexity is defined as



where H() is the Shannon entropy of  measured in bits 



The perplexity can be interpreted as a smooth measure of the effective number of neighbors. The performance of SNE is fairly robust to changes in the perplexity, and typical values are between 5 and 50.

The minimization of the cost function is performed using gradient decent. And physically, the gradient may be interpreted as the resultant force created by a set of springs between the map point and all other map points  . All springs exert a force along the direction ( – ). The spring between  and repels or attracts the map points depending on whether the distance between the two in the map is too small or too large to represent the similarities between the two high-dimensional datapoints. The force exerted by the spring between and  is proportional to its length, and also proportional to its stiffness, which is the mismatch (pj|i – qj|i + p i| j − q i| j ) between the pairwise similarities of the data points and the map points[1].-
