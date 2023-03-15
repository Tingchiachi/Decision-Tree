<div align='center'>

# Decision tree

</div>
note  

1. **Motivation**

    Decision tree can be applied to both regression and classification.  
    These involve *stratifying* or *segmenting* the predictor space into a number of simple regions.  
    Tree-based methods are simple and useful for interpretation.

2. **Different between regression and classification**
    <div class = "center">

    |     |regression|classification|
    |:---:|:--------:|:------------:|
    |variable type|quantitative|qualitative|
    |recursive binary splitting|RSS|Impurity|

    </div>

3. **Constructing a tree(recursive binary splitting)**

   * RSS  
      predictor space:$R_1,R_2,...,R_J$
      $$RSS=\sum_{j=1}^{J}\sum_{i\in R_j}(y_i-\hat{y}_{R_j})^2$$
      where $\hat{y}_{R_j}$ is the mean(mode,median) for observations within the $j$th region.  
      $\Rightarrow$ Minimize the **RSS**

   * Impurity
        * classification error rate
       $$E=1-max_k(\hat p_{mk})$$
        * Gini Index
       $$G=\sum_{k=1}^K\hat p_{mk}(1-\hat p_{mk})$$
        * entropy
       $$D=-\sum_{k=1}^K\hat p_{mk}log(\hat p_{mk})$$

     $\hat p_{mk}$ represents the proportion of observations in the $m$th region that are from the $k$the class.  
     Gini Index and entropy are more sensitive than classification error rate.  
     **(Important)** You must check original RSS or Impurity before spliting the node.

4. **Pruning the tree**  
   To avoid growing a very large tree(over-fitting)
     * Cost complexity pruning(Weakest link pruning)
   $$\sum_{m=1}^{|T|}\sum_{i:x_i\in R_m}(y_i-\hat{y}_{R_m})^2+\alpha |T|$$
   *Tree score* = *RSS* + *Complexity penalty*,which $\alpha$ is determined by Cross-Validation,$|T|$ is the number of leaves.  
   Step:
       1. Use recursive binary splitting to grow a large tree

       2. Apply Cost complexity pruning to obtain a sequence of $\alpha$,starting with $\alpha = 0$ and increasing it to find the best subtree to minimize *Tree score*,untill $|T|=1$.

       3. Use *K*-fold cross-validation to choose $\alpha$:  
       (a) Repeat step 1 and 2 on all but the $k$ th fold of the training data, $k = 1,\dots,K$  
       (b) Evaluate RSS or accuracy on the $k$ th testing data  
       (c) Calculating every $\alpha$'s RSS or accuracy average,finally pick the final $\alpha$ has the lowest RSS or the highest accuracy.

       4. Use the final $\alpha$ to construct the tree.
5. **Advantages and Disadvantages of dicision tree**
   * Advantages
      * easy to explain
      * graphically and visually
      * non-expert can easily understand
      * tree can handle quantitative and qualitative variable
      * tree can handle highly non-linear and complex relationship
   * Disadvantages
      * tree generally do not have the same level of predictive accuracy as some of the other regression and classification method
      * tree can be very non-robust
