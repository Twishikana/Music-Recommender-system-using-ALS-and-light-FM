
## The data set

In this project, we'll use the [Goodreads dataset](https://sites.google.com/eng.ucsd.edu/ucsdbookgraph/home) collected by 
> Mengting Wan, Julian McAuley, "Item Recommendation on Monotonic Behavior Chains", RecSys 2018.


## Basic recommender system

This recommendation model uses Spark's alternating least squares (ALS) method to learn latent factor representations for users and items.
This model has some hyper-parameters that should be tune to optimize performance on the validation set, notably: 

  - the *rank* (dimension) of the latent factors, and
  - the regularization parameter *lambda*.
  
 We further use light FM to integrate the concepts of collaborative and content based recommenders.

### Data splitting and subsampling

For this project, the data splitting was as follows:
  -  60% of users (and all of their interactions) to form the *training set*.
  -  20% of users to form the *validation set*.  For each validation user, use half of their interactions for training, and the other half should be held out for validation.  (Remember: you can't predict items for a user with no history at all!)
  - Remaining users: same process as for validation.

In general, users with few interactions (say, fewer than 10) may not provide sufficient data for evaluation, especially after partitioning their observations into train/test.
We discarded these users from the experiment

## Extensions
   - *Comparison to single-machine implementations*: compared Spark's parallel ALS model to a single-machine implementation, e.g. lightfm. Our comparison measures both effeciency (model fitting time as a function of data set size) and resulting accuracy.
