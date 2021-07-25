This repository contains evaluation dataset for targeted sentiment analysis (TSA).
This dataset contains sentences from other datasets that cannot be re-distributed in clear text. 
That's why the included file **tsa_evaluation_hidden.json** contains IDs instead of sentence texts. 

You need to download the resources from the other datasets and run the script that restores the texts as described below.
The resulting file **tsa_evaluation.json** will contain the sentences with annotated targets and sentiments.

The file contains a JSON array of examples, where each example includes the sentence text and a list of targets. 
A target includes the text, its location in the sentence, and the sentiment. 
The sentiment value can be **positive**, **negative**, **mixed**, or **none**.

An example looks like this:
```json
  {
    "text": "Great food but the service was dreadful !",
    "targets": [
      {
        "text": "food",
        "location": {
          "begin": 6,
          "end": 10
        },
        "sentiment": "positive"
      },
      {
        "text": "service",
        "location": {
          "begin": 19,
          "end": 26
        },
        "sentiment": "negative"
      }
    ]
  }
```

License
---
This dataset is released under Community Data License Agreement – Sharing, Version 1.0 (https://cdla.dev/sharing-1-0/)

Downloading dataset resources
---

### Download Yelp dataset
Follow the instructions at https://www.yelp.com/dataset/download

Choose Download JSON at "Download The Data" page

Use path to the file **yelp_academic_dataset_review.json** as value for argument  **--yelp**, for example:  
```commandline
--yelp ~/Downloads/yelp_dataset/yelp_academic_dataset_review.json
```

### Download English test file from Multilingual Amazon Reviews Corpus
Access the data as described here: https://docs.opendata.aws/amazon-reviews-ml/readme.html#access 

Download the test file https://amazon-reviews-ml.s3-us-west-2.amazonaws.com/json/test/dataset_en_test.json
and use its path as value for argument **--amazon**:
```commandline
--amazon ~/Downloads/dataset_en_test.json
```

### Download SST dataset
Download the data set from  https://nlp.stanford.edu/sentiment/index.html 
("Main zip file" link on the right side: http://nlp.stanford.edu/~socherr/stanfordSentimentTreebank.zip) and unzip it.

Use the directory path as value for argument **--sst**:
```commandline
--sst ~/Downloads/stanfordSentimentTreebank
```

### Download Opinosis dataset
Download from the repository https://github.com/kavgan/opinosis-summarization file `OpinosisDataset1.0_0.zip` and unzip it.

Use the path of **topics** directory as value for argument **--opinosis**:
```commandline
--opinosis ~/Downloads/OpinosisDataset1.0/topics
```

### Download SemEval14 ABSA Test Data
Go to the MetaShare site at http://metashare.elda.org/repository/browse/semeval-2014-absa-test-data-gold-annotations/b98d11cec18211e38229842b2b6a04d77591d40acd7542b7af823a54fb03a155/
login, download and unzip the data file.

Use the path of the directory as value for argument **--semeval**:
```commandline
--semeval ~/Downloads/ABSA_Gold_TestData
```

Run restore script
-----------------
Script requirements:
* Python 3
* pandas
* nltk


Run the script `restore_texts.py` with the arguments described above.
All the arguments are optional, if you skip an argument for a source, its sentences will not be restored. 

```commandline
python restore_texts.py \
    --yelp ~/Downloads/yelp_dataset/yelp_academic_dataset_review.json \
    --amazon ~/Downloads/dataset_en_test.json \
    --sst ~/Downloads/stanfordSentimentTreebank \
    --opinosis ~/Downloads/OpinosisDataset1.0/topics \
    --semeval ~/Downloads/ABSA_Gold_TestData 
```

The dataset with restored sentences is saved to the file `tsa_evaluation.json`

