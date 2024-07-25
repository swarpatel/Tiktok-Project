# **TikTok Project**

Welcome to the TikTok Project!

You have just started as a data professional at TikTok.

The team is still in the early stages of the project. You have received notice that TikTok's leadership team has approved the project proposal. To gain clear insights to prepare for a claims classification model, TikTok's provided data must be examined to begin the process of exploratory data analysis (EDA).

**Inspect and analyze data**

**The goal** is to construct a dataframe in Python, perform a cursory inspection of the provided dataset, and inform TikTok data team members of your findings.
<br/>
*This project has three parts:*

**Part 1:** Understand the situation
* How can you best prepare to understand and organize the provided TikTok information?

**Part 2:** Understand the data

* Create a pandas dataframe for data learning and future exploratory data analysis (EDA) and statistical activities

* Compile summary information about the data to inform next steps

**Part 3:** Understand the variables

* Use insights from your examination of the summary data to guide deeper investigation into variables

<br/>


# **Identify data types and compile summary information**


Throughout these project notebooks, you'll see references to the problem-solving framework PACE. The following notebook components are labeled with the respective PACE stage: Plan, Analyze, Construct, and Execute.

<img src="images/Pace.png" width="100" height="100" align=left>

# **PACE stages**

</br></br></br>

<img src="images/Plan.png" width="100" height="100" align=left>


## **PACE: Plan**


### **Task 1. Understand the situation**

#### How can you best prepare to understand and organize the provided information?


●	Who is your audience for this project? 

    TikTok data team and cross-functional team members.

●	What are you trying to solve or accomplish? And, what do you anticipate the impact of this work will be on the larger needs of the client? 

    Development of a predictive model that can be used to determine whether a video contains a claim or whether it offers an opinion.

●	What questions need to be asked or answered?

    What is the condition of the provided dataset? 
    What variables will be the most useful? 
    Are there trends within the data that can provide insight? 
    What steps can I take to reduce the impact of bias?

●	What resources are required to complete this project? 

    Project dataset, Python notebook, and input from stakeholders.

●	What are the deliverables that will need to be created over the course of this project? 

    Dataset scrubbed for exploratory data analysis, visualizations, statistical model, regression analysis and/or machine learning model.


<img src="images/Analyze.png" width="100" height="100" align=left>

## **PACE: Analyze**

</br></br>

### **Task 2a. Imports and data loading**




```python
# Import packages
import pandas as pd
import numpy as np
```

Then, load the dataset into a dataframe. Creating a dataframe will help conduct data manipulation, exploratory data analysis (EDA), and statistical activities.


```python
# Load dataset into dataframe
data = pd.read_csv("tiktok_dataset.csv")
```

### **Task 2b. Understand the data - Inspect the data**

*Consider the following questions:*

**Question 1:** When reviewing the first few rows of the dataframe, what do you observe about the data? What does each row represent?

**Question 2:** When reviewing the `data.info()` output, what do you notice about the different variables? Are there any null values? Are all of the variables numeric? Does anything else stand out?

**Question 3:** When reviewing the `data.describe()` output, what do you notice about the distributions of each variable? Are there any questionable values? Does it seem that there are outlier values?


```python
# Display and examine the first ten rows of the dataframe
data.head(10)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>claim_status</th>
      <th>video_id</th>
      <th>video_duration_sec</th>
      <th>video_transcription_text</th>
      <th>verified_status</th>
      <th>author_ban_status</th>
      <th>video_view_count</th>
      <th>video_like_count</th>
      <th>video_share_count</th>
      <th>video_download_count</th>
      <th>video_comment_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>claim</td>
      <td>7017666017</td>
      <td>59</td>
      <td>someone shared with me that drone deliveries a...</td>
      <td>not verified</td>
      <td>under review</td>
      <td>343296.0</td>
      <td>19425.0</td>
      <td>241.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>claim</td>
      <td>4014381136</td>
      <td>32</td>
      <td>someone shared with me that there are more mic...</td>
      <td>not verified</td>
      <td>active</td>
      <td>140877.0</td>
      <td>77355.0</td>
      <td>19034.0</td>
      <td>1161.0</td>
      <td>684.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>claim</td>
      <td>9859838091</td>
      <td>31</td>
      <td>someone shared with me that american industria...</td>
      <td>not verified</td>
      <td>active</td>
      <td>902185.0</td>
      <td>97690.0</td>
      <td>2858.0</td>
      <td>833.0</td>
      <td>329.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>claim</td>
      <td>1866847991</td>
      <td>25</td>
      <td>someone shared with me that the metro of st. p...</td>
      <td>not verified</td>
      <td>active</td>
      <td>437506.0</td>
      <td>239954.0</td>
      <td>34812.0</td>
      <td>1234.0</td>
      <td>584.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>claim</td>
      <td>7105231098</td>
      <td>19</td>
      <td>someone shared with me that the number of busi...</td>
      <td>not verified</td>
      <td>active</td>
      <td>56167.0</td>
      <td>34987.0</td>
      <td>4110.0</td>
      <td>547.0</td>
      <td>152.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>claim</td>
      <td>8972200955</td>
      <td>35</td>
      <td>someone shared with me that gross domestic pro...</td>
      <td>not verified</td>
      <td>under review</td>
      <td>336647.0</td>
      <td>175546.0</td>
      <td>62303.0</td>
      <td>4293.0</td>
      <td>1857.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>claim</td>
      <td>4958886992</td>
      <td>16</td>
      <td>someone shared with me that elvis presley has ...</td>
      <td>not verified</td>
      <td>active</td>
      <td>750345.0</td>
      <td>486192.0</td>
      <td>193911.0</td>
      <td>8616.0</td>
      <td>5446.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>claim</td>
      <td>2270982263</td>
      <td>41</td>
      <td>someone shared with me that the best selling s...</td>
      <td>not verified</td>
      <td>active</td>
      <td>547532.0</td>
      <td>1072.0</td>
      <td>50.0</td>
      <td>22.0</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>claim</td>
      <td>5235769692</td>
      <td>50</td>
      <td>someone shared with me that about half of the ...</td>
      <td>not verified</td>
      <td>active</td>
      <td>24819.0</td>
      <td>10160.0</td>
      <td>1050.0</td>
      <td>53.0</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>claim</td>
      <td>4660861094</td>
      <td>45</td>
      <td>someone shared with me that it would take a 50...</td>
      <td>verified</td>
      <td>active</td>
      <td>931587.0</td>
      <td>171051.0</td>
      <td>67739.0</td>
      <td>4104.0</td>
      <td>2540.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Get summary info
data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 19382 entries, 0 to 19381
    Data columns (total 12 columns):
     #   Column                    Non-Null Count  Dtype  
    ---  ------                    --------------  -----  
     0   #                         19382 non-null  int64  
     1   claim_status              19084 non-null  object 
     2   video_id                  19382 non-null  int64  
     3   video_duration_sec        19382 non-null  int64  
     4   video_transcription_text  19084 non-null  object 
     5   verified_status           19382 non-null  object 
     6   author_ban_status         19382 non-null  object 
     7   video_view_count          19084 non-null  float64
     8   video_like_count          19084 non-null  float64
     9   video_share_count         19084 non-null  float64
     10  video_download_count      19084 non-null  float64
     11  video_comment_count       19084 non-null  float64
    dtypes: float64(5), int64(3), object(4)
    memory usage: 1.8+ MB
    


```python
# Get summary statistics
data.describe()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>#</th>
      <th>video_id</th>
      <th>video_duration_sec</th>
      <th>video_view_count</th>
      <th>video_like_count</th>
      <th>video_share_count</th>
      <th>video_download_count</th>
      <th>video_comment_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>19382.000000</td>
      <td>1.938200e+04</td>
      <td>19382.000000</td>
      <td>19084.000000</td>
      <td>19084.000000</td>
      <td>19084.000000</td>
      <td>19084.000000</td>
      <td>19084.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>9691.500000</td>
      <td>5.627454e+09</td>
      <td>32.421732</td>
      <td>254708.558688</td>
      <td>84304.636030</td>
      <td>16735.248323</td>
      <td>1049.429627</td>
      <td>349.312146</td>
    </tr>
    <tr>
      <th>std</th>
      <td>5595.245794</td>
      <td>2.536440e+09</td>
      <td>16.229967</td>
      <td>322893.280814</td>
      <td>133420.546814</td>
      <td>32036.174350</td>
      <td>2004.299894</td>
      <td>799.638865</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>1.234959e+09</td>
      <td>5.000000</td>
      <td>20.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>4846.250000</td>
      <td>3.430417e+09</td>
      <td>18.000000</td>
      <td>4942.500000</td>
      <td>810.750000</td>
      <td>115.000000</td>
      <td>7.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>9691.500000</td>
      <td>5.618664e+09</td>
      <td>32.000000</td>
      <td>9954.500000</td>
      <td>3403.500000</td>
      <td>717.000000</td>
      <td>46.000000</td>
      <td>9.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>14536.750000</td>
      <td>7.843960e+09</td>
      <td>47.000000</td>
      <td>504327.000000</td>
      <td>125020.000000</td>
      <td>18222.000000</td>
      <td>1156.250000</td>
      <td>292.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>19382.000000</td>
      <td>9.999873e+09</td>
      <td>60.000000</td>
      <td>999817.000000</td>
      <td>657830.000000</td>
      <td>256130.000000</td>
      <td>14994.000000</td>
      <td>9599.000000</td>
    </tr>
  </tbody>
</table>
</div>



### 1. Observations about the data from looking at the first 10 rows

    Claim Status: Each row represents a video associated with a "claim". The claim_status indicates the current state of the claim related to the video (e.g., "claim")
</br>
    Video ID: Each row has a unique identifier for the video, represented by the video_id
</br>
    Video Duration: The duration of each video is given in seconds by the video_duration_sec
</br>
    Video Transcription: The video_transcription_text column provides a textual transcript of the video content
</br>
    Verification and Ban Status: The verified_status indicates if the video is verified, and the author_ban_status shows the ban status of the author
</br>
    Engagement Metrics: The dataset includes several metrics related to video engagement:
</br>
    video_view_count: Number of views
</br>
    video_like_count: Number of likes
</br>
    video_share_count: Number of shares
</br>
    video_download_count: Number of downloads
</br>
    video_comment_count: Number of comments
</br>
    Each row, therefore, represents a single video along with its associated claim status, verification status, ban status, and various engagement metrics.

### 2. Data Info Observations

    Non-null Counts: 
There are some missing values in the columns claim_status, video_transcription_text, video_view_count, video_like_count, video_share_count, video_download_count, and video_comment_count.

    claim_status: 
19084 non-null values out of 19382.

    video_transcription_text: 
19084 non-null values out of 19382.

    The engagement metrics (video_view_count, video_like_count, video_share_count, video_download_count, video_comment_count) also have 19084 non-null values.

    Data Types: 
The data types vary among the columns:

    Numeric columns: 
#, video_id, video_duration_sec, video_view_count, video_like_count, video_share_count, video_download_count, video_comment_count (with video_view_count, video_like_count, video_share_count, video_download_count, video_comment_count being float64, and the rest int64).

    Object columns: 
claim_status, video_transcription_text, verified_status, author_ban_status.

    Potential Issues: 
The presence of null values in key columns and the mix of data types.

### 3. Descriptive Statistics Observations

    Counts: 
The count for numeric columns #, video_id, and video_duration_sec is consistent at 19382, but for the engagement metrics, it is 19084, indicating missing data.

    Means and Medians:

The mean video_duration_sec is approximately 32.42 seconds.

The mean values for engagement metrics are significantly higher than the median (50th percentile), suggesting skewed distributions with some very high values.

    Standard Deviations: 
The high standard deviations in video_view_count, video_like_count, video_share_count, video_download_count, and video_comment_count indicate high variability.

    Min and Max Values:

The minimum values for engagement metrics (views, likes, shares, downloads, comments) are 0 or very low.

The maximum values are very high, especially for video_view_count (999,817), video_like_count (657,830), video_share_count (256,130), video_download_count (14,994), and video_comment_count (9,599).

    Potential Outliers: 
The large range and high maximum values compared to the median suggest the presence of outliers in the engagement metrics.

    In summary, the dataset contains a mixture of numeric and categorical data with some missing values and potential outliers, particularly in the engagement metrics. This initial review helps in understanding the overall structure and variability within the dataset, setting the stage for more detailed analysis and potential data cleaning steps.

### **Task 2c. Understand the data - Investigate the variables**

A good first step towards understanding the data might be examining the `claim_status` variable.


```python
# What are the different values for claim status and how many of each are in the data?
data['claim_status'].value_counts()
```




    claim_status
    claim      9608
    opinion    9476
    Name: count, dtype: int64



**Question:** What do you notice about the values shown?

    The counts of each claim status are quite balanced.

Next, examine the engagement trends associated with each different claim status.

Start by using Boolean masking to filter the data according to claim status, then calculate the mean and median view counts for each claim status.


```python
# What is the average view count of videos with "claim" status?
claims = data[data['claim_status'] == 'claim']
print('Mean view count claims:', claims['video_view_count'].mean())
print('Median view count claims:', claims['video_view_count'].median())
```

    Mean view count claims: 501029.4527477102
    Median view count claims: 501555.0
    


```python
# What is the average view count of videos with "opinion" status?
opinions = data[data['claim_status'] == 'opinion']
print('Mean view count opinions:', opinions['video_view_count'].mean())
print('Median view count opinions:', opinions['video_view_count'].median())
```

    Mean view count opinions: 4956.43224989447
    Median view count opinions: 4953.0
    

**Question:** What do you notice about the mean and media within each claim category?

* Both categories (claims and opinions) show symmetry in their view count distributions, as indicated by the close proximity of their mean and median values.

* Videos labeled as claims have significantly higher view counts (both mean and median) compared to those labeled as opinions.

* The view counts for opinions are much lower on average, indicating that opinions might be less popular or less frequently viewed compared to claims.

* The close proximity of mean and median values within each category suggests that the data distributions for view counts are not heavily skewed by extreme values.

Now, examine trends associated with the ban status of the author.

Use `groupby()` to calculate how many videos there are for each combination of categories of claim status and author ban status.


```python
# Get counts for each group combination of claim status and author ban status
data.groupby(['claim_status', 'author_ban_status']).count()[['#']]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>#</th>
    </tr>
    <tr>
      <th>claim_status</th>
      <th>author_ban_status</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">claim</th>
      <th>active</th>
      <td>6566</td>
    </tr>
    <tr>
      <th>banned</th>
      <td>1439</td>
    </tr>
    <tr>
      <th>under review</th>
      <td>1603</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">opinion</th>
      <th>active</th>
      <td>8817</td>
    </tr>
    <tr>
      <th>banned</th>
      <td>196</td>
    </tr>
    <tr>
      <th>under review</th>
      <td>463</td>
    </tr>
  </tbody>
</table>
</div>



**Question:** What do you notice about the number of claims videos with banned authors? Why might this relationship occur?

    Higher Proportion of Claims by Banned Authors:

Claims made by banned authors (1439) are relatively high compared to opinions by banned authors (196). This suggests that banned authors are more likely to have made claims rather than opinions.

    Lower Proportion of Opinions by Banned Authors:

Opinions by banned authors are significantly lower compared to the claims by banned authors.

    Review Process:

There are a substantial number of claims and opinions under review (1603 claims and 463 opinions). This indicates an active review process, which might be linked to the ban status of authors.

**Potential Reasons for the Relationship:**

    Content Policy Violations:

Authors who make claims might be more likely to violate content policies, leading to bans. Claims could be more prone to scrutiny and thus more likely to result in bans compared to opinions.

    Nature of Content:

Claims might involve more controversial or sensitive content, leading to higher chances of policy violations and subsequent bans compared to opinions, which might be perceived as less factual and more subjective.

    Platform Policies:

The platform may have stricter enforcement or review mechanisms for claims, increasing the likelihood that authors making claims are banned.

    User Behavior:

Authors prone to being banned might be those who make more claims rather than opinions, possibly due to a tendency to assert controversial or unverified information.
    
Understanding these relationships helps in identifying potential areas for improving content moderation and user management policies on the platform.

</br>

Continue investigating engagement levels, now focusing on `author_ban_status`.

Calculate the median video share count of each author ban status.


```python
data.groupby(['author_ban_status']).agg(
    {'video_view_count': ['mean', 'median'],
     'video_like_count': ['mean', 'median'],
     'video_share_count': ['mean', 'median']})
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">video_view_count</th>
      <th colspan="2" halign="left">video_like_count</th>
      <th colspan="2" halign="left">video_share_count</th>
    </tr>
    <tr>
      <th></th>
      <th>mean</th>
      <th>median</th>
      <th>mean</th>
      <th>median</th>
      <th>mean</th>
      <th>median</th>
    </tr>
    <tr>
      <th>author_ban_status</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>active</th>
      <td>215927.039524</td>
      <td>8616.0</td>
      <td>71036.533836</td>
      <td>2222.0</td>
      <td>14111.466164</td>
      <td>437.0</td>
    </tr>
    <tr>
      <th>banned</th>
      <td>445845.439144</td>
      <td>448201.0</td>
      <td>153017.236697</td>
      <td>105573.0</td>
      <td>29998.942508</td>
      <td>14468.0</td>
    </tr>
    <tr>
      <th>under review</th>
      <td>392204.836399</td>
      <td>365245.5</td>
      <td>128718.050339</td>
      <td>71204.5</td>
      <td>25774.696999</td>
      <td>9444.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# What's the median video share count of each author ban status?
data.groupby(['author_ban_status']).median(numeric_only=True)[['video_share_count']]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>video_share_count</th>
    </tr>
    <tr>
      <th>author_ban_status</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>active</th>
      <td>437.0</td>
    </tr>
    <tr>
      <th>banned</th>
      <td>14468.0</td>
    </tr>
    <tr>
      <th>under review</th>
      <td>9444.0</td>
    </tr>
  </tbody>
</table>
</div>



**Question:** What do you notice about the share count of banned authors, compared to that of active authors? Explore this in more depth.

    Banned authors have a median share count that's 33 times the median share count of active authors.
    
    The high share count for banned authors suggests that there is a significant engagement with their content before it gets banned. This highlights the challenges in content moderation, particularly in balancing engagement with policy compliance. The platform might benefit from proactive moderation strategies to address potentially violating content before it reaches high levels of engagement.

Use `groupby()` to group the data by `author_ban_status`, then use `agg()` to get the count, mean, and median of each of the following columns:
* `video_view_count`
* `video_like_count`
* `video_share_count`

Remember, the argument for the `agg()` function is a dictionary whose keys are columns. The values for each column are a list of the calculations you want to perform.


```python
data.groupby(['author_ban_status']).agg(
    {'video_view_count': ['count', 'mean', 'median'],
     'video_like_count': ['count', 'mean', 'median'],
     'video_share_count': ['count', 'mean', 'median']
     })
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="3" halign="left">video_view_count</th>
      <th colspan="3" halign="left">video_like_count</th>
      <th colspan="3" halign="left">video_share_count</th>
    </tr>
    <tr>
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>median</th>
      <th>count</th>
      <th>mean</th>
      <th>median</th>
      <th>count</th>
      <th>mean</th>
      <th>median</th>
    </tr>
    <tr>
      <th>author_ban_status</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>active</th>
      <td>15383</td>
      <td>215927.039524</td>
      <td>8616.0</td>
      <td>15383</td>
      <td>71036.533836</td>
      <td>2222.0</td>
      <td>15383</td>
      <td>14111.466164</td>
      <td>437.0</td>
    </tr>
    <tr>
      <th>banned</th>
      <td>1635</td>
      <td>445845.439144</td>
      <td>448201.0</td>
      <td>1635</td>
      <td>153017.236697</td>
      <td>105573.0</td>
      <td>1635</td>
      <td>29998.942508</td>
      <td>14468.0</td>
    </tr>
    <tr>
      <th>under review</th>
      <td>2066</td>
      <td>392204.836399</td>
      <td>365245.5</td>
      <td>2066</td>
      <td>128718.050339</td>
      <td>71204.5</td>
      <td>2066</td>
      <td>25774.696999</td>
      <td>9444.0</td>
    </tr>
  </tbody>
</table>
</div>



**Question:** What do you notice about the number of views, likes, and shares for banned authors compared to active authors?

* `Banned authors have significantly higher mean and median views compared to active authors.`
* `Banned authors have substantially higher mean and median likes compared to active authors.`
* `Banned authors also have higher mean and median shares compared to active authors.`


Now, create three new columns to help better understand engagement rates:
* `likes_per_view`: represents the number of likes divided by the number of views for each video
* `comments_per_view`: represents the number of comments divided by the number of views for each video
* `shares_per_view`: represents the number of shares divided by the number of views for each video


```python
# Create a likes_per_view column
data['likes_per_view'] = data['video_like_count'] / data['video_view_count']

# Create a comments_per_view column
data['comments_per_view'] = data['video_comment_count'] / data['video_view_count']

# Create a shares_per_view column
data['shares_per_view'] = data['video_share_count'] / data['video_view_count']
```

Use `groupby()` to compile the information in each of the three newly created columns for each combination of categories of claim status and author ban status, then use `agg()` to calculate the count, the mean, and the median of each group.


```python
data.groupby(['claim_status', 'author_ban_status']).agg(
    {'likes_per_view': ['count', 'mean', 'median'],
     'comments_per_view': ['count', 'mean', 'median'],
     'shares_per_view': ['count', 'mean', 'median']})
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th colspan="3" halign="left">likes_per_view</th>
      <th colspan="3" halign="left">comments_per_view</th>
      <th colspan="3" halign="left">shares_per_view</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>median</th>
      <th>count</th>
      <th>mean</th>
      <th>median</th>
      <th>count</th>
      <th>mean</th>
      <th>median</th>
    </tr>
    <tr>
      <th>claim_status</th>
      <th>author_ban_status</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">claim</th>
      <th>active</th>
      <td>6566</td>
      <td>0.329542</td>
      <td>0.326538</td>
      <td>6566</td>
      <td>0.001393</td>
      <td>0.000776</td>
      <td>6566</td>
      <td>0.065456</td>
      <td>0.049279</td>
    </tr>
    <tr>
      <th>banned</th>
      <td>1439</td>
      <td>0.345071</td>
      <td>0.358909</td>
      <td>1439</td>
      <td>0.001377</td>
      <td>0.000746</td>
      <td>1439</td>
      <td>0.067893</td>
      <td>0.051606</td>
    </tr>
    <tr>
      <th>under review</th>
      <td>1603</td>
      <td>0.327997</td>
      <td>0.320867</td>
      <td>1603</td>
      <td>0.001367</td>
      <td>0.000789</td>
      <td>1603</td>
      <td>0.065733</td>
      <td>0.049967</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">opinion</th>
      <th>active</th>
      <td>8817</td>
      <td>0.219744</td>
      <td>0.218330</td>
      <td>8817</td>
      <td>0.000517</td>
      <td>0.000252</td>
      <td>8817</td>
      <td>0.043729</td>
      <td>0.032405</td>
    </tr>
    <tr>
      <th>banned</th>
      <td>196</td>
      <td>0.206868</td>
      <td>0.198483</td>
      <td>196</td>
      <td>0.000434</td>
      <td>0.000193</td>
      <td>196</td>
      <td>0.040531</td>
      <td>0.030728</td>
    </tr>
    <tr>
      <th>under review</th>
      <td>463</td>
      <td>0.226394</td>
      <td>0.228051</td>
      <td>463</td>
      <td>0.000536</td>
      <td>0.000293</td>
      <td>463</td>
      <td>0.044472</td>
      <td>0.035027</td>
    </tr>
  </tbody>
</table>
</div>



**Question:**

How does the data for claim videos and opinion videos compare or differ? Consider views, comments, likes, and shares.

* Videos by banned authors and those under review generally receive significantly more views, likes, and shares compared to videos by active authors. However, when a video is viewed, the engagement rate depends more on the video's claim status than the author's ban status.

* Claim videos attract more views and likes on average than opinion videos, indicating that claim videos are more positively received. They also generate more comments and shares than opinion videos.

* For claim videos, banned authors have slightly higher likes-to-views and shares-to-views ratios compared to active authors or those under review. Conversely, for opinion videos, active authors and those under review achieve higher engagement rates in all categories than banned authors.

<img src="images/Construct.png" width="100" height="100" align=left>

## **PACE: Construct**

**Note**: The Construct stage does not apply to this workflow.




<img src="images/Execute.png" width="100" height="100" align=left>

## **PACE: Execute**


### **Given your efforts, what can you summarize for Rosie Mae Bradshaw and the TikTok data team?**

*Note for Learners: Your answer should address TikTok's request for a summary that covers the following points:*

*   What percentage of the data is comprised of claims and what percentage is comprised of opinions?

    `Out of the 19,382 samples in this dataset, around 50% are claims, totaling 9,608.`

*   What factors correlate with a video's claim status?

    `Engagement levels are highly correlated with claim status, warranting further investigation.`

*   What factors correlate with a video's engagement level?

    `Videos by banned authors exhibit significantly higher engagement than those by active authors, with videos by authors under review displaying engagement levels between the two.`

