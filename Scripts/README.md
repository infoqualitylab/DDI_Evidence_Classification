## Python Programs Description

### Program 1 – “Getting_articles_metadata.ipynb”
* This script is used to get metadata of the articles which were used in our project. The metadata is collected from PubMed API including: article PubMed ID, title, abstract, publication type and Mesh headings.
* Input: a text file that contains a list of PubMed Identifiers of papers (Available in Data folder: All_Papers_PMIDs.txt)
* Output: an Excel file that contains the papers with their metadata (Available in Data folder: All_Papers_Metadata.xlsx)

### Program 2 – “Preprocess_fulltext_articles.ipynb”
* This script contains 3 sub-programs:
  - A program to convert full-text papers from PDFs to plaintext
  - A program to extract text of “Methods” sections from the plaintext papers
  - A program to preprocess the text of “Methods” sections

* Sub-program 1: convert full-text papers from PDFs to plaintext
  - Use PDFMiner package (applicable with Python 3.7)
  - Input: path to a folder that contains PDF papers (that we used for this project)
  - Output: path to a folder that you plan to store the plaintext papers 
  - For each PDF file in the input folder, the program generates a corresponding plaintext file in the output folder. Note that not all PDF files are allowed to read and convert to text (e.g. PDF files are actually images). For such PDFs, we manually opened the file and saved the text as plaintext.

* Sub-program 2: extract text of “Methods” sections from the plaintext papers
  - Input: path to a folder that you contains plaintext papers (resulted from sub-program 1)
  - Output: path to a folder that you plan to store the plaintext of Methods sections. 
  - For each plaintext file in the input folder, the program extracted text of the Methods section and save into a single file named with “Methods_section” + PMID of the paper. 

* Sub-program 3: preprocess the Methods section text 
  - Input: path to a folder that you contains plaintext files of Methods section
  - Output: “clean” plaintext files of Methods section
  - Preprocess: remove stopwords (using NLTK), remove spaces and some special characters

*NOTE: Output of this step is a single csv file that contains all papers, their metadata (collected by script 1) and Methods section text (collected by script 2) (Available in Data folder: All_Papers_Preprocessed.csv. Note that this file also contains expert’s labels for classification development)

### Program 3 – “Most_informative_unigrams.ipynb”

* This script is used to get lists of most informative features (unigrams) from our data (text from title, abstract & method section); selected based on the TFIDF scores of the features. 
* Input: the All_Papers_Preprocessed.csv file. Note that this file also contains expert’s labels for classification development. 
* Output: lists of 20 most informative unigrams for each type in the six evidence types of the study. 

Script 4 - “Multiclass_classifier.ipynb”

Implement the multi class classifier to predict six evidence types (no hierarchy involved). 
Input: the All_Papers_Preprocessed.csv file.
Classifier implementation: 
Data: split training 80%; testing 20%
Features: unigrams of text from Title, Abstract, Methods section (TFIDF)
Feature selection: top 5000 best features by Chi-square test
ML model: SVM
Evaluation metrics: Accuracy, Precision, Recall, F1 score (note: AUC ROC is not applicable for multi class problem)
Evaluate classifier on a set of unlabeled dataset: 
Save the classification model and rerun it on an unlabeled dataset
Input: text from title, abstract & methods section of unlabeled papers. 
Output: prediction of what evidence types the papers provide. 
Script 5 - “Hierarchical_classifier.ipynb”

Implement the hierarchical classifier to predict six evidence types
Input: the All_Papers_Preprocessed.csv file.
Classifier implementation: 
Cross-validation: 5 folds 
In each cross validation: 
Data: split training 80%; testing 20%
Start from top-level sub-classifier to lower-level sub-classifiers. 
Features: unigrams of text from Title, Abstract, Methods section (TFIDF)
Feature selection: top 5000 best features by Chi-square test
ML model: SVM
Evaluation metrics: Accuracy, Precision, Recall, F1 score and AUC ROC of sub-classifiers individually. 
Evaluate classifier on a set of unlabeled dataset: 
Save the classification model and rerun it on an unlabeled dataset
Input: text from title, abstract & methods section of unlabeled papers. 
Output: prediction of what evidence types the papers provide. 
