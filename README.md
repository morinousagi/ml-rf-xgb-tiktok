# Classifying TikTok videos using machine learning

(Google Advance Data Analytics Course 6)

## Project
To develop a model to predict whether a TikTok video presents a `claim` or an `opinion`.

- A `claim` requires further human intervention.
- An `opinion` does not require human intervention.
- A `claim` that is misclassified as an `opinion` is highly undesirable.

Therefore, the aim would be identifying a `claim` video as a `positive` outcome.

## Target variable

- ***claim_status***: identifies which are `claim` videos for further human intervention.

## Evaluation approach

- Minimal false negatives i.e. misclassifying a claim as opinion
- Important model evaluation metric, Recall = TP / (TP+FN)

## EDA

Not displayed in the Jupyter Notebook
```
- data.head(10)
- data.shape
- data.info()
- data.describe()
- data.isnull().sum()
```
Explored outliers using box plots. In social network or security threat datasets, outliers could be crucial in anomaly detection. Therefore, there is no handling of outliers in this dataset. Tree-based models can handle outliers well.

Additional viz: [Tableau](https://public.tableau.com/app/profile/morinousagi/viz/Courseproject_17585318018580/Story1)

## Contents of `gada-project-tiktok.ipynb`

### Feature engineering
- Feature creation: char length of `video_transcription_text`
- Feature encoding: dummy encode categorical values
- Feature selection: drop unnecessary columns 

### Split data
- training/validation/testing: 60/20/20
- `stratify=y` even though classes are balanced

### Models: Random Forest & XGBoost
- GridSearchCV, refit=`recall`
- Hyperparameters tuning

### Evaluation
- Confusion Matrix
- classification_report

Both models offer almost the same performance, with rf_cv performs slightly better than xgb_cv.
To explore more features to potentially lower false negatives further.

- Use champion model to predict on test data
- Feature importances of champion model


## Data dictionary

Dataset: *tiktok_dataset.csv*
- contains synthetic data created for this project in partnership with TikTok
- **19,383 rows** – each row represents a different published TikTok video in which a claim/opinion has been made
- **12 columns** - as shown below

| Column name | Type | Description |
| ----------- | -------- | -------- | 
| # | int | TikTok assigned number for video with claim/opinion |
| claim_status | obj | Whether the published video has been identified as an “opinion” or a “claim.” In this dataset, an “opinion” refers to an individual’s or group’s personal belief or thought. A “claim” refers to information that is either unsourced or from an unverified source. |
| video_id  | int | Random identifying number assigned to video upon publication on TikTok |
| video_duration_sec | int | How long the published video is measured in seconds |
| video_transcription_text | obj | Transcribed text of the words spoken in the published video |
| verified_status | obj | Indicates the status of the TikTok user who published the video in terms of their verification, either “verified” or “not verified” |
| author_ban_status | obj | Indicates the status of the TikTok user who published the video in terms of their permissions: “active,” “under scrutiny,” or “banned” |
| video_view_count | float | The total number of times the published video has been viewed |
| video_like_count | float | The total number of times the published video has been liked by other users |
| video_share_count | float | The total number of times the published video has been shared by other users |
| video_download_count | float | The total number of times the published video has been downloaded by other users |
| video_comment_count | float | The total number of comments on the published video |
