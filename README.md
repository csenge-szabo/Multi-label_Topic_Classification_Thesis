# Multi-label Topic Classification of Client Feedback in the Governance Domain 

## A Thesis Project by *Csenge Szabó* 
## Master's Degree in 'Linguistics: Text Mining', Vrije Universiteit Amsterdam 2023/2024

This repository belongs to the Master's Thesis Project "*Multi-label Topic Classification of Client Feedback in the Governance Domain*" by Csenge Szabó, supervised by Dr. Ilia Markov and Sandra Blok. 
The project was carried out in collaboration with the company [MarketResponse](https://marketresponsegroup.com/), a Dutch software company specializing in CX analytics in order to bridge the gap between customer feedback and business performance.

The thesis focuses on the multi-label topic classification of written client feedback collected from the governance domain through surveys. Multi-label topic classification involves assigning more than one topic label to a particular text instance from a predefined set of topics. For this purpose, we compare a traditional machine learning classifier ([Support Vector Machines](https://scikit-learn.org/stable/modules/svm.html))) with a more recent transformer-based model (fine-tuned [BERT](https://huggingface.co/google-bert/bert-base-uncased)) that currently shows state-of-the-art performance for the majority of Natural Language Processing tasks. Since the topic labels in the dataset are structured into main topics and corresponding subtopics, we experiment with one-step and two-step classification approaches. The former implies the classification of instances for all topic labels at once, while the latter means first predicting main topic labels and then subtopic labels. In order to address the imbalanced nature of the dataset, various data adaptation and data balancing techniques are explored, namely (i) undersampling aimed to reduce the prevalence of overrepresented subtopic classes to the average distribution, and (ii) oversampling aimed to generate synthetic data for underrepresented subtopic classes using a generative large language model, GPT-4. We aim to determine the best approach for multi-label topic classification on the provided dataset using a combination of the aforementioned approaches.

The motivation, methodology, results and discussion of the results can be found in the [thesis report](https://github.com/csenge-szabo/Multi-label_Topic_Classification_Thesis/blob/main/MA_Thesis_Csenge_Szabo.pdf). 

**Note:** Since the data cannot be shared with third-parties, it is not published in this repository. Outputs that give an indication about its content have been hidden.

## Content

### Folder Structure 
```
Thesis Project Structure 
└───code
│       |   preprocessing.py
        |   data_adaptation.py
        |   SVMs_1step.py
        |   SVMs_2step.py
        |   BERT_1step.ipynb
        |   BERT_2step.ipynb
        |   utils.py
        |   error_analysis.py
└───data
│       │   example_dataset.csv
└───figures
│   └───SVMs_1step
│   └───SVMs_2step
│   └───SVMs_2step_oversampled
│   └───SVMs_2step_undersampled
│   └───BERT_1step
│   └───BERT_2step
│   └───BERT_2step_oversampled
│   └───BERT_2step_undersampled
└───hyperparameters
└───model_predictions
└───models
└───results
│   └───BERT
│   └───SVMs
│   .gitignore
│   LICENSE
│   README.md
│   requirements.txt
```

### \code
The [code](https://github.com/csenge-szabo/Multi-label_Topic_Classification_Thesis/tree/main/code) folder contains the scripts and  notebooks required to reproduce this study.
In order to reproduce the experiments, follow the order of the files listed below:

For pre-processing: 
* `preprocessing.py` cleans the dataset from privacy-sensitive information (names, dates, times, locations, URLs, e-mail addresses). It pre-processes the dataset by applying lowercasing and stop words removal. It implements Binary Relevance problem transformation in order to convert the labels into 0 and 1. It conducts stratified data splitting in a ratio of 80-10-10 (train-validation-test).

* `statistics.ipynb` generates statistics regarding the full annotated dataset. It also includes code to inspect the label distribution in the split data (train-validation-test).

For data adaptation: 
* `data_adaptation.py` undersamples the training dataset for the overrepresented main topics until they reach the average distribution, or can be used to pre-process the synthetic data generated by GPT-4.

Multi-label Topic Classification Task: 
* `SVMs_1step.py` trains a Support Vector Machines classifier, conducts hyper-parameter tuning and predicts the labels on the test set using TF-IDF feature representation. The script is designed for one-step classification, i.e. main topics and subtopics are learned and predicted in a single step. The script can be used with the original, undersampled or oversampled training data. The default for this script is the original training set.

* `SVMs_2step.py` trains a Support Vector Machines classifier, conducts hyper-parameter tuning and predicts the labels on the test set using TF-IDF feature representation. The script is designed for two-step classification, i.e. first the model is used to predict main topics, then to predict the corresponding subtopics using the output of the first phase. The script can be used with the original, undersampled or oversampled training data. The default for this script is the original training set.

* `BERT_1step.ipynb` fine-tunes a pre-trained BERT model on the training set, which has to be specified within the notebook by uncommenting certain parts. The default for this notebook is the original training set. The script is designed for one-step classification, i.e. main topics and subtopics are learned and predicted in a single step. The fine-tuned model is then saved to the models folder.
    * This script uses the helper functions stored in `utils.py`

* `BERT_2step.ipynb` fine-tunes a pre-trained BERT model on the training set, which has to be specified within the notebook by uncommenting certain parts. The default for this notebook is the original training set. The script is designed for two-step classification, i.e. first the model is used to predict main topics, then to predict the corresponding subtopics using the output of the first phase. The fine-tuned model is then saved to the models folder.
    * This script uses the helper functions stored in `utils.py`

For error analysis: 
* `error_analysis.py` allows you to inspect often confused topic labels, and can be used to look up a specific test instance (based on instance ID) to check its gold and predicted labels.

### \data
The [data](https://github.com/csenge-szabo/Multi-label_Topic_Classification_Thesis/tree/main/data) folder only contains the `example_dataset.csv` since the data is not allowed to be shared due to the confidentiality agreement. However, the CSV file represents the structure of the data.

### \figures
The [figures](https://github.com/csenge-szabo/Multi-label_Topic_Classification_Thesis/tree/main/figures) folder is used to store the figures, for instance, the confusion matrices of each classification approach. It is separated into the different approaches and each contains the corresponding confusion matrices:

* \BERT_1step
* \BERT_2step
* \BERT_2step_oversampled
* \BERT_2step_undersampled
* \SVMs_1step
* \SVMs_2step
* \SVMs_2step_oversampled
* \SVMs_2step_undersampled

### \hyperparameters
The [hyperparameters](https://github.com/csenge-szabo/Multi-label_Topic_Classification_Thesis/tree/main/hyperparameters) folder is used to store pickle files, which contain information about the optimal hyper-parameter settings for the one-step and two-step SVMs model. 

### \model_predictions
The [model_predictions](https://github.com/csenge-szabo/Multi-label_Topic_Classification_Thesis/tree/main/model_predictions) folder contains the model outputs, i.e. CSV files with the feedback statements from the test data, and their predicted labels. Due to the confidentiality restrictions, the files were not uploaded.

### \models
The [models](https://github.com/csenge-szabo/Multi-label_Topic_Classification_Thesis/tree/main/models) folder is a location for the trained models. Due to the confidentiality restrictions and the size of the models, the models were not uploaded.

### \results
The [results](https://github.com/csenge-szabo/Multi-label_Topic_Classification_Thesis/tree/main/results) folder contains the results, i.e., the classification reports. The reports can be found in `\BERT` and `\SVMs`.
* \BERT
    * `test_report_1step.csv`
    * `test_report_2step.csv`
    * `test_report_2step_undersampled.csv`
    * `test_report_2step_oversampled.csv`
* \SVMs
    * `test_report_1step.csv`
    * `test_report_2step.csv`
    * `test_report_2step_undersampled.csv`
    * `test_report_2step_oversampled.csv`

### `requirements.txt`
This txt file lists all the required packages. 
***

## Thesis Report
### `MA_Thesis_Csenge_Szabo.pdf`
The pdf file contains the full thesis report.
***

# References
The code for the conventional machine learning approach was partially inspired by Piek Vossen, [Source Code](https://github.com/cltl/ma-hlt-labs/tree/master/lab3.machine_learning).

The code to fine-tune the BERT model was adapted from [Abhishek Kumar Mishra](https://github.com/abhimishra91/transformers-tutorials/blob/master/transformers_multi_label_classification.ipynb), who used it for multi-label text classification of toxic data.
