# kaggle-2023-cia-hackathon-solution

## Competition
https://www.kaggle.com/competitions/2023ActPaHatExpert

This hackathon was hosted by The Canadian Institute of Actuaries (CIA), the CAS Institute (iCAS), and the Society of Actuaries (SOA) and the it took place from March 23-16 in 2023.

The problem set is NLP task and the datasets contain (mostly) recent tweets from high profile Twitter accounts in the fields of blockchain, cryptocurrency, and Web3. Participants were tasked to make predictions on the number of retweets and likes for each tweet.


## Overview of 2nd place solution

I used XGBoost for my solusion and the final submission is an ensemble of three different XGBoost predictions (XGBoost1, XGBoost2 and XGBoost3) with weights of 0.2, 0.2 and 0.6.

Final prediction = xgb_v18_count * 0.2 + xgb_v18_reglinear * 0.2 + xgb_v18_reglinear_rooty * 0.6

Each of XGBoost models were built based on the same set of features, and differences are "objective" parameter and target variable transformation as below. The reason why I did this is because target variable is highly skewed and I thought that linear regression may not work well and also it may be better to transform target variable as well.
| script                        | objective     | y transformation | Public LB |
| ----------------------------- | ------------- | ---------------- | --------- |
| xgb_v18_count.ipynb           | reg:linear    | y                | 1515.96x  |
| xgb_v18_reglinear.ipynb       | count:poisson | y                | NA        |
| xgb_v18_reglinear_rooty.ipynb | reg:linear    | y^(1/2)          | 1510.55x  |

The public/private leaderboard scores are as follows.
| script                        | Public LB | Private LB |
| ----------------------------- | ----------| ---------- |
| ensemble_avg_v04.ipynb        | 1508.49x  | 523.65x    |


## Things that didn't work out

Since this is NLP task, I attempted to build NLP model with DeBERTa base model. However, the public LB score was not good at all (1644.86x).
It may be because the target variable is highly skewed and NLP model may not work well in this case.
