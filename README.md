### Facebook checkin prediction
In this project we study the Facebook checkin prediction on Kaggle. We are given about 30 million simulated checkin
datas on a 10X10 map. The features are the x, y coordinates of checkin locations, time and accuracy. Besides x, y, 
we are not given any descriptions about the features. The goal is to predict the business id that the user will check in,
given the features.

#### Analysis
Quite intuitively, the most import features are location. For example, we randomly take a look of an area we can see lot
of clustering patterns.

![Clustering](https://github.com/jimmychou0704/Facebook/blob/master/popular_area.png)

Once we fix a neighborhood, we can see the effect by time. For example, the left hand side consits of  checkin in 
"early time", while the right hand side are checkin in "late time". We can see the majority of blue points appears 
in the "late time".

![Early_late](https://github.com/jimmychou0704/Facebook/blob/master/early_late.png)

To predict the checkins, we first figure out the training data points close the test point given. Then we use these neighbor
training points to train model. So it is important to find "close points" in an efficient way. To this aim, we use the data 
structure QuadTree to save the training set. Then the searching costs log N time complexity. We can see from the following 
table how much we can improve the accuracy using this QuadTree data structure, comparing to plain application of machine learning 
algorithm.



| Number of datas  |    58000 |  116000 |  291180 |
| -------------    |    ------|---------|------   |
| Number of labels |    38071 |  57000  |  83345  |
| Plain KNN        |    0.09  |  0.02   |  0.02   |  
| QuadTree         |    0.23  |  0.11   |  0.09   |
