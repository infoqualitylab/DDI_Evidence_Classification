# DDI_Evidence_Classification
Combine machine learning and knowledge representation to facilitate the process of assessing evidence from studies of drug-drug interaction by using an existing ontology of evidence types (e.g. DDI clinical trials vs. pharmacokinetic trials), as the backbone to develop a series of classifiers that categorize a DDI study’s evidence type based on its textual characteristics.

Download the source codes from the GitHub site:
https://github.com/infoqualitylab/DDI_Evidence_Classification/ 

### GitHub folder contains 2 sub-folders:
- Data: contains all data files that are used/generated throughout the project.

- Scripts: contains all Python scripts that are developed to implement the project. Python scripts are used to preprocess data, generate features and develop machine learning models. 

### Environment
- Programming Language: Python (version 3.0)

- Please make sure that you have the following programs on your machine in order to run the script:

       + Python 3.0: https://www.python.org/downloads/
       
       + Jupyter Notebook: http://jupyter.org/install

### Python scripts

#### Script 1 – “Getting_articles_metadata.ipynb” 

- This script is used to get metadata of the articles which were used in our project. The metadata is collected from PubMed API, including: article PubMed ID, title, abstract, publication type and Mesh headings. 

- The script takes the input which is a plaintext file which contains the list of PMIDs of the articles being used in the project (/Data/Articles_PMIDs.txt). 

- In order to run the script, replace the variable “PMID_list_file” to the path to the “Data” folder where the “Articles_PMIDs.txt” is located. 

- Output of the script is an Excel file that contains all articles and their metadata (/Data/Articles_Metadata.xlsx)
 
#### Script 2 – “Preprocess_fulltext_articles.ipynb”

- This script is used to programmatically convert full-text articles from PDFs to plaintext and extract text from “Methods” section of the articles. 

- The script contains 3 functions:

   + Convert PDFs to plaintext files: takes input which are full-text articles in PDFs and produces output which are the full-text articles in plaintext format.
   
   + Get the “Methods” sections from the plaintext files: takes input which are full-text articles in plaintext and produces output which are text of the “Methods” sections in plaintext format. 
o	Preprocess text of the Methods section: eliminate special characters, stop words, numbers. 

#### Script 3 – “Extract_Drug_Entities_MetaMap_Results.ipynb”
