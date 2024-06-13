# ASE_Submit
This is a replication package for "Detecting Missing Information of Questions in Q&A Chatrooms".

Goal: Automatically assess the quality of the questions in developer chatrooms by detecting missing information (ETD and PS)
- Problem Statement (PS) — A summary of the program's malfunction or any problematic scenario currently encountered by the user.
- Expect to Do (ETD) — A summary outlining the anticipated behavior of the program or other expectations from the user.

## 1 File Structure
In folder "data/", important files are: 
- Pattern_Catalog_66.xlsx: Pattern Catelog of 66 lexico-syntactic patterns based on 1000 questions in the pattern discovery set
- PatternDiscovery_1000.csv: Pattern discovery set of 1,000 questions, artifacts from open coding procedure, including maunally identified sentences containing ETD/PS, pattern_code of summarized patterns, labels
- Validation_1000.csv: Validation set of 1,000 questions, validation results from Heuristic approach, including predicted patterns and corresponding predicted labels

In folder "code/":
- Hueristic_NLP.zip: Implementation for the heuristic approach
- SVM.ipynb: Implementation for the SVM approach
- Pretrained_Detection.ipynb: Implementation for the pre-trained models
- Pretrained_withPattern_Detection.ipynb: Implementation for the pre-trained models with pattern features added
- OpenAI_Detect.ipynb: Implementation for CoT Prompting on GPT-3.5 Turbo and GPT-4o

In folder "experiment/", three sub-folders are:
- svm: Validation results from the SVM approach (Table 4 in the paper)
- pretrained: Validation results from the pre-trained models (Table 4 in the paper)
- OpenAI: Validation results from the LLMs (Table 5 and 7 in the paper)

## 2 Dataset Summary
A sample set of approximately 5,000 questions extracted from over 21K issue-solution pairs published by Shi et al., covering eight active domains on Gitter: front end framework, mobile, data science, DevOps, blockchain platform, collaboration, web app, and programming language. A dataset of 2,000 questions were curated after preprocessing (e.g., noise filtering) and then two subsets were created from these:
- Pattern discovery set: 1,000 questions were used for lexico-syntactic pattern discovery for ETD and PS.
- Validation set: Remaining 1,000 questions for validation purposes.

## 3 Techniques Summary
Four automated approaches were designed and evaluated to detect missing ETD and/or PS in chatroom questions:
- Heuristic: Employ part-of-speech (POS) tagging and heuristics to align sentences with 66 lexico-syntactic patterns. Labels an question as containing ETD/PS if and only if at least one pattern is applicable to at least one of the sentences in the question.
- SVM: Employ two types of features, lexico-syntactic patterns and n-grams. For patterns, each ETD and PS pattern is defined as a boolean feature indicating its presence or absence in any of the sentences within a chatroom question. For n-grams, unigrams, bigrams, and trigrams were applied, where each n-gram is defined as a boolean feature indicating its presence or absence in any of the sentences within a chatroom question.
- Pre-trained: Employ three state-of-the-art pre-trained models from TensorFlow Hub, namely BERT, RoBERTa, and ELECTRA. Additional version of pre-trained models where each of them will be provided with hand-crafted features derived from the lexico-syntactic patterns in the same way as in the SVM experiments.
- Prompting: Employ Chain-of-Thought (CoT) prompting in combination with two state-of-the-art LLMs, GPT-3.5 Turbo and GPT-4o.

## 4 Replication Process
To replicate the Heuristic approach:
- Requirements: Java and IntelliJ IDEA Community Edition installed
- Input Files: "issue.csv", "tag_dict.csv" and "Pattern_code_list.csv" in "data/"
- Steps to reproduce:
  - Unzip the file "Hueristic_NLP.zip" in "code/"
  - Import this project into IntelliJ
  - Specify the output path in line 30 for variable "outputPath"
  - Run the project
  - Results saved in "../data/Validation_1000.csv" (columns "predicted_PS" and "predicted_ETD" are generated patterns, columns "y_PS" and "y_ETD" are the ground truth, columns "y'_PS" and "y'_ETD" are the predicted labels)

To replicate the SVM approach:
- Requirements: Anaconda intalled (make sure jupyter notebook or jupyterLab installed), Packages (scikit-learn, pandas, numpy) installed
- Input Files: "Validation_1000.csv" in folder "data/"
- Steps to reproduce:
  - Launch jupyter notebook or jupyterLab and then run "SVM.ipynb" in "code/"
  - Run all the cells sequentially
  - The dataset of 10-fold cross-validation is created in "../data/cross_validate_10/"
  - All results saved in "../experiment/svm/"
 
To replicate the Pre-trained (with/without pattern features) models:
- Requirements: Anaconda intalled (make sure jupyter notebook or jupyterLab installed), Packages (tensorflow2 with GPU, scikit-learn, pandas, numpy) installed
- Input Files: The dataset of 10-fold cross-validation in "../data/cross_validate_10/" (created in the SVM approach)
- Steps to reproduce:
  - Launch jupyter notebook or jupyterLab and then run "Pretrained_Detection.ipynb" or "Pretrained_withPattern_Detection.ipynb" in "code/"
  - Run all the cells sequentially
  - All results saved in "../experiment/pretrained/"

To replicate the CoT Prompting on LLMs:
- Requirements: Anaconda intalled (make sure jupyter notebook or jupyterLab installed), Packages (OpenAI, scikit-learn, pandas, numpy) installed, an account created in OpenAI platform and get the OpenAI API key
- Input Files: "issue.csv" in "data/", different versions of system message in "data/prompt/" and examples in "data/prompt/example"
- Steps to reproduce:
  - Launch jupyter notebook or jupyterLab and then run "OpenAI_Detect.ipynb" in "code/"
  - Run all the cells sequentially
  - All results saved in "../experiment/OpenAI/"
