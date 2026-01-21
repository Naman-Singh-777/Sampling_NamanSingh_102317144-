## About this Assignment

So this assignment was about dealing with imbalanced datasets. You know how sometimes you have way more data for one class than another? That was the case here with credit card fraud data.

The dataset I got had like 763 normal transactions but only 9 fraud cases. When you try to train a model on this, it just predicts everything as normal because that's what it sees most. Not useful at all.

## What I Had to Do

First thing was to balance this data. Used RandomOverSampler for that - basically it copies the minority class samples until both classes have same number. After that I had 763 of each (total 1526 rows).

Then the actual work started. Had to create 5 different samples:
1. Simple random - just pick random rows
2. Systematic - every kth row
3. Stratified - keeps the class ratio same  
4. Cluster - divide into groups then sample
5. Bootstrap - random with replacement (same row can appear multiple times)

Sample size I used was 152 rows which is around 10% of the balanced data.

After creating samples, tested 5 models on each:
- Logistic Regression (M1)
- Decision Tree (M2)  
- Random Forest (M3)
- SVM (M4)
- KNN (M5)

## Results

Here's what I got:

| Model | Sampling1 | Sampling2 | Sampling3 | Sampling4 | Sampling5 |
|-------|-----------|-----------|-----------|-----------|-----------|
| M1    | 86.96     | 80.43     | 93.48     | 86.67     | 91.30     |
| M2    | 95.65     | 97.83     | 97.83     | 95.56     | 97.83     |
| M3    | 97.83     | 97.83     | 95.65     | 97.78     | 100.00    |
| M4    | 86.96     | 80.43     | 91.30     | 91.11     | 91.30     |
| M5    | 73.91     | 82.61     | 82.61     | 91.11     | 89.13     |

Random Forest hit 100% with bootstrap. Pretty good.

## Some Things I Noticed

M3 (Random Forest) worked really well with bootstrap sampling - got perfect accuracy. Makes sense I guess because Random Forest already does bootstrap stuff internally.

Decision Tree was stable. Got 97.83% with like three different sampling methods. Didn't matter much which one.

Logistic Regression liked stratified sampling best (93.48%). Probably because it keeps the balance right which helps linear models.

KNN was all over the place. Started at 73.91% with simple random but jumped to 91.11% with cluster sampling. I think KNN really depends on how the data points are arranged so different sampling affected it a lot.

SVM did okay. Best was 91.30% with stratified and bootstrap.

## What This Means

Tree models (Decision Tree and Random Forest) don't really care that much about which sampling you use. They're pretty robust.

Random Forest was consistently good no matter what. If I had to pick just one model for this, that would be it.

But the interesting thing is KNN - it really varied a lot. So for KNN you'd have to be more careful about your sampling technique.

## Running This

To run the code:
1. Clone repo
2. `pip install -r requirements.txt`
3. Put the dataset file in the right place
4. Run the script
5. Check results.csv

## Conclusion

So yeah, main takeaway is that sampling technique matters but it depends on your model. Random Forest with bootstrap gave best results (100%) but Decision Tree was also really consistent across the board.

For KNN you really need to think about which sampling to use because it makes a big difference. Linear models like Logistic Regression seem to prefer stratified.

If you're not sure which model to use, Random Forest is probably your safest bet because it works well regardless of sampling method.



