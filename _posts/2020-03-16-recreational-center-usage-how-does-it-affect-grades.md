---
title: "Recreational center usage: how does it affect grades?"
date: "2020-03-16"
categories: 
  - "classification"
  - "data-science"
  - "python3"
tags: 
  - "pandas"
  - "python"
  - "statistics"
---

I was fortunate to get access to a large volume of data of student swipes at my university's recreational center. This is all swipes for a complete academic year, anonymized of course.

<script src="https://gist.github.com/ajey091/0d6fbcabe7e7e9b58c690212484d4719.js"></script>

![Screen Shot 2020-03-16 at 12.15.16 PM.png](/assets/images/screen-shot-2020-03-16-at-12.15.16-pm.png)

![Screen Shot 2020-03-16 at 12.16.53 PM.png](/assets/images/screen-shot-2020-03-16-at-12.16.53-pm.png)

### Exploratory data analysis and data cleaning

Pandas Profiling has been a game-changer since I found it. Excellent to get a good first dive into the data.

<script src="https://gist.github.com/ajey091/2aa0e7fb5ed777a190b73e6c7ba78bc9.js"></script>

![Screen Shot 2020-03-16 at 12.18.37 PM.png](/assets/images/screen-shot-2020-03-16-at-12.18.37-pm.png)

![Screen Shot 2020-03-16 at 12.20.13 PM.png](/assets/images/screen-shot-2020-03-16-at-12.20.13-pm.png)

![Screen Shot 2020-03-16 at 12.21.34 PM.png](/assets/images/screen-shot-2020-03-16-at-12.21.34-pm.png)

Yikes, that's 60 columns. But there are a lot of columns that are highly collinear and some others that are missing a lot of values. We will remove these as they contain no information. We will use the results from our earlier profiling to select the columns to delete. We will remove all columns that have >50% missing values, which is not a totally unreasonable thing to do. It also happens that it is intuitively unlikely for these columns to have any effect on the outcome.

### Frequency of use versus student GPA

<script src="https://gist.github.com/ajey091/368b0af29ab8b92e150d1c17ae0eca68.js"></script>

![corec1.png](/assets/images/corec1.png)

This is a fantastic early indication that the frequency of use is strongly correlated with GPA.

`data['Type of User'].value_counts()`

![Screen Shot 2020-03-16 at 12.26.37 PM.png](/assets/images/screen-shot-2020-03-16-at-12.26.37-pm.png)

It looks like these classes are imbalanced.

### Role of gender

<script src="https://gist.github.com/ajey091/61bd6b350d300785a36b2d95ae7fd28a.js"></script>

![corec2.png](/assets/images/corec2.png)

### International students

<script src="https://gist.github.com/ajey091/e39642fa167fdf084ed5f5f22e8ff9f0.js"></script>

![corec3.png](/assets/images/corec3.png)

Surprising to me that international students have such a high average GPA compared to domestic students.

<script src="https://gist.github.com/ajey091/71982d1fed847e3ed7264dbbd48695b1.js"></script>

![Screen Shot 2020-03-16 at 12.31.40 PM.png](/assets/images/screen-shot-2020-03-16-at-12.31.40-pm-1.png)

![Screen Shot 2020-03-16 at 12.31.46 PM.png](/assets/images/screen-shot-2020-03-16-at-12.31.46-pm-1.png)

It seems that being a regular recreational center user has a more pronounced influence on the GPA for women.

<script src="https://gist.github.com/ajey091/9d5a6778835d722a0b6ca5e8d40adda0.js"></script>

![corec4.png](/assets/images/corec4.png)

There is definitely some weak correlation between number of swipes and overall GPA.

<script src="https://gist.github.com/ajey091/da8532c2f25396e1a574d0f6d7dfc07e.js"></script>

![corec5.png](/assets/images/corec5.png)

<script src="https://gist.github.com/ajey091/c7245cdc1f2e9b0d12b09960d8f06869.js"></script>

![corec6.png](/assets/images/corec6.png)

Graduate students tend to be more active.

### Honors students

<script src="https://gist.github.com/ajey091/6a210ca73fa7ae90bf20bacf6f7b2a12.js"></script>

![Screen Shot 2020-03-16 at 1.18.10 PM.png](/assets/images/screen-shot-2020-03-16-at-1.18.10-pm.png)

![corec7.png](/assets/images/corec7.png)

### Let's try to predict GPA classes

<script src="https://gist.github.com/ajey091/f6a0acadd59d41b16b6fef0c8b219fd1.js"></script>

![Screen Shot 2020-03-16 at 1.19.20 PM.png](/assets/images/screen-shot-2020-03-16-at-1.19.20-pm.png)

<script src="https://gist.github.com/ajey091/90325d7da5d8973c64696584b83007a1.js"></script>

```
Total Features:  25 categorical + 15 numerical = 40 features
```

<script src="https://gist.github.com/ajey091/66c02e28ad5ccbe275e017824cd4ebe2.js"></script>

![Screen Shot 2020-03-16 at 1.21.43 PM.png](/assets/images/screen-shot-2020-03-16-at-1.21.43-pm.png)

We have to be careful about how we handle the missing values - for instance, NaN for residence hall could just mean that the student did not use on-campus housing. So, NaN in that case could actually provide useful information. From the above breakdown, this is what we will plan to do with the NaN values:

1. Geocluster: Impute with mode
2. Citizenship type: Leave as is- i.e., forms a unique value of its own
3. Academic School Grouping, Program: Impute with mode
4. Year GPA: Impute with median
5. Semester Honors: Leave as is
6. Spring Credits Attempted, Spring Credits Earned, Spring GPA: impute with median All this magic happens below:

<script src="https://gist.github.com/ajey091/22106e1b2912fb4eeed7e9e4a5ecd89b.js"></script>

Now we are on to encoding the features. The categorical features are encoded using OneHotEncoder, the output is encoded using Label encoder.

<script src="https://gist.github.com/ajey091/b08e78a31c27891bd085b26c1840d1e6.js"></script>

![Screen Shot 2020-03-16 at 1.23.16 PM.png](/assets/images/screen-shot-2020-03-16-at-1.23.16-pm.png)

Looks great. Let's train and test then. We will start with a dummy classifier.

<script src="https://gist.github.com/ajey091/d68e4565359afc938df22d107a91da31.js"></script>

![Screen Shot 2020-03-16 at 1.26.06 PM.png](/assets/images/screen-shot-2020-03-16-at-1.26.06-pm.png)

<script src="https://gist.github.com/ajey091/1e526b40aa1dddd56bbda829f3c8662b.js"></script>

![Screen Shot 2020-03-16 at 1.26.44 PM.png](/assets/images/screen-shot-2020-03-16-at-1.26.44-pm.png)

<script src="https://gist.github.com/ajey091/fd793a3a56e5b523ace3c96c3e48e4a7.js"></script>

![Screen Shot 2020-03-16 at 1.27.39 PM.png](/assets/images/screen-shot-2020-03-16-at-1.27.39-pm.png)

<script src="https://gist.github.com/ajey091/20523caa92c4813289fc9ab509f909d0.js"></script>

![Screen Shot 2020-03-16 at 1.28.20 PM.png](/assets/images/screen-shot-2020-03-16-at-1.28.20-pm.png)

We are not done yet. Our results are strongly dependent on the test/train split of our dataset. Based on the input `random_state` value, our prediction parameters will vary. We can address this by running the model on a bunch of test/train datasets as below:

<script src="https://gist.github.com/ajey091/2fcf3f0f863f8b708eca68d47fc770eb.js"></script>

![corec8.png](/assets/images/corec8-1.png)

![corec9.png](/assets/images/corec9.png)

The above distribution provides us confidence that the predicted accuracy and F1 score are in the same range as we saw previously.

### Conclusion

The moral of the story is "Study hard but also make sure you stay physically active". And also, we can predict your GPA with 72% accuracy. It seems like staying physically active has a non-trivial effect on academic performance.

Following were some of the interesting observations:

1. In general, student who use the rec center regularly had a higher average GPA.
2. Female students have a higher average GPA than male counterparts and the effect of being a heavy rec center user are more pronounced for them.
3. International students tend to have higher average GPA.
4. Honors students use the rec center more and have a higher than average GPA.
5. We can predict the GPA class of a student from other characteristics and frequency of use with a reasonable accuracy (72%).
