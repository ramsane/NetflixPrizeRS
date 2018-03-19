# Netflix Prize - Rating Prediction

- The Netflix Prize was an open competition for the best algorithm to predict user ratings for films, based on previous ratings without any other information about the users or films, i.e. without the users or the films being identified except by numbers assigned for the contest.

- This way of predicting new ratings of (user, movie) pair is called  __Collaborative filtering__ 

-  the grand prize was __$1,000,000__ and was won by BellKor's Pragmatic Chaos team. __Our dataset is the dataset that was used in that competition.__


- __TRAINING DATASET__
    - No. of Ratings : 100 Million 
    - No. of Users   : 480k users
    - No of Movies   : 17k movies
    

- We can't handle this much data at once. Our System will crash or We will run out of memory.

- What we did is:
  - Because we are given with timestamps also.., we can sort the data with the timestamp.
  - Since we don't have actual ratings of test data, we will divide the Original Train Data into train and Test data.
  - We will perform different models on the New_Train_Data and evaluate our model with New_Test_Data (both are atually from Original_Train_Data)


- __NEW_TRAIN_DATA__:
    - It has around 80 Million ratings


- __NEW_TEST_DATA__ :
     - It has around 20 Million ratings
     
- __COLD START CASES__ :
    - New Users  :  75148(15.65 %) 
    - New Movies : 346(1.95 %) 


## My Approach of solving: 

- Since we can't do any experiments on such huge data.., we sampled few points from the New_Train and New_Test, and we will analyse different models. 

- It was done in __3 stages__.
  - First with small sample
  - Next with Medium sample
  - Finally, we will analyse the whole data
 

- - - - - - - - - - - - - 

### 1. Small Sample 
- __Train Data__ :
     - Ratings : 129286
     - Users   : 10,000
     - Movies  : 1,000

- __Test Data__:
     - Ratings : 7333
     - Users   : 5,000
     - Movies  : 500

- __Cold Start Cases__:: 18.765%

- __Least_RMSE__ : 1.078365 (with single level blending... with XGBoost)

- - - - - - - - - - - - - 

### 2. Medium Sample 

- __Train Data__ :
     - Ratings : 473343
     - Users   : 20,000
     - Movies  : 2,000

- __Test Data__ :
     - Ratings : 111758
     - Users   : 10,000
     - Movies  : 3,500

- __Cold Start Cases__: 48.23%

- __Least_RMSE__ : 1.0578 (XGBoost _just with_ engineered features. )

- - - - - - - - - - - - - 

### 3. Whole data

- __Train Data__ :
     - Ratings : 8038440532 
     - Users   : 405041
     - Movies  : 17424

- __Test Data__ :
     - Ratings : 20096102
     - Users   : 349312
     - Movies  : 17757

- __Cold Start Cases__:
    - With movies : 1.95 % (346)
    - With users  : 15.65 % (75148)
 
- __Least_RMSE__ : 0.986832 (using just SVD)
- - - - - - - - - - - - - - 
### Engineered Features for XGBoost:

- __GAvg__ : Average rating of all the ratings 
- __Similar users rating of this movie__:
    - sur1, sur2, sur3, sur4, sur5 ( top 5 simiular users who rated that movie.. )

- __Similar movies rated by this user__:
    - smr1, smr2, smr3, smr4, smr5 ( top 5 simiular movies rated by this movie.. )
- __UAvg__ : User AVerage rating
- __MAvg__ : Average rating of this movie
- __rating__ : Rating of this movie by this user.
