# Sequence Aware Recommenders: Sensitivity perturbations of the sequence

#### Federico Chung: fchung12@uw.edu, Charles Reinertson: crein1@uw.edu, Ernesto Cediel: eced@uw.edu

#### March 2023

## Please see Project_Report.pdf for full paper

## Introduction

A very strong assumption of any usage of data is that the data has no errors. However, due to
many issues/edge cases in the data collection process, there can be violations of this assumption.
This is no different for movie recommender systems which in some cases collect their data through
explicit feedback. Explicit feedback sequences are collected through user feedback mechanisms such
as user ratings. However, the point in time when they consumed or purchased an item might be
quite different from the time they rated an item [3].
Another potential way movie data can be unintentionally perturbed is due to the rating of random
movies within a sequence. This might be due to many causes such as account/password sharing. A
recent study estimates that 22.6 % of people engage in password sharing in the US [2]. This means
that we cant ensure that movie lists are from one user but of multiple users.
This paper tries to explore the potential effects of different levels of perturbations on recommender
systems. By using different levels of imputation and order perturbations we try to understand the
limitations of recommender systems when we find perturbed datasets. We want to better understand
how these sequence-aware recommender systems perform in these edge-case scenarios, and how well-
equipped they are to deal with them.

## Conclusion

The CASER (CNN) greatly outperforms the BST in all of our evaluation metrics. This is because the
CASER (CNN) embeds a target sequence of T items from the user watch history. The BST, however,
only embeds the next item as the target item. The BST is therefore learning to predict the very
next item’s rating the best it can, whereas the CASER (CNN) learns to predict a target sequence
that aligns more favorably with the evaluation metrics Precision@k, Recall@k, and NDCG@k. The
BST has a final feed-forward network with the last layer having length one. This is because it learns
to predict the ratings of unseen movies through Mean Squared Error Loss between the predicted
movie rating (the final network layer) and the actual movie rating. This is not directly learning an
ordered sequence recommendation task that we are evaluating. The CASER’s loss function is much
more favorable to this task. The output of the last layer of the CASER (CNN) are scores of a user
watching each and every movie. Binary cross-entropy loss is then used to learn the probabilistic
sequence of these scores.
Because of the above limitations of the BST, we chose to limit our conclusions to findings only
related to the CASER (CNN). The CASER (CNN) is robust against random shuffling of data but
performs poorly with data imputations. This is because random shuffling does not change the most
important signal, the movies that a user watches. Although the sequence of the movies is important
and shuffling this sequence causes performance degradation, this is not the most important model
signal.
The CASER (CNN), according to the paper [4], exhibits skip behavior that allows the model to
be robust enough to make sensible recommendations despite imputed user-watch history sequences.
However, the benefits of skip behavior are not readily seen when we perform data imputations.
The more we impute random movies in the sequence, the worse the CASER (CNN) performs in
this recommendation task. We see a negative, exponential decay to linear correlation between the
percentage of random movies imputed and model performance over recall, precision, and NDCG.
In general, the benefits of sequence-aware recommender models compared to their sequence-
agnostic counterparts are small. The correct, non-imputed information is much more important
than the signal from the order of the sequence. More research must be done to harness the benefits
of sequential patterns for recommendation systems.


## References

[1] Sejoon Oh, Berk Ustun, Julian McAuley, and Srijan Kumar. Rank list sensitivity of recommender
systems to interaction perturbations. InProceedings of the 31st ACM International Conference
on Information & Knowledge Management, pages 1584–1594, 2022.

[2] Niko Pajkovic. Algorithms and taste-making: Exposing the netflix recommender system’s oper-
ational logics.Convergence, 28(1):214–235, 2022.

[3] Massimo Quadrana, Paolo Cremonesi, and Dietmar Jannach. Sequence-aware recommender
systems.ACM Computing Surveys (CSUR), 51(4):1–36, 2018.

[4] Jiaxi Tang and Ke Wang. Personalized top-n sequential recommendation via convolutional se-
quence embedding. InProceedings of the eleventh ACM international conference on web search
and data mining, pages 565–573, 2018.
