# ASE_Submit
Automatically assess the quality of the questions in developer chatrooms by detecting missing information (ETD and PS)

## 1 Dataset Summary
In folder "data/", files should be: 
(1) Pattern_Catalog_66.xlsx: Pattern Catelog of 66 lexico-syntactic patterns based on 1000 questions in the pattern discovery set
(2) PatternDiscovery_1000.csv:  Pattern discovery set of 1,000 questions, includes artifacts from open coding procedure, maunally identified sentences containing ETD/PS, pattern_code from summarized patterns, labels
(3) Validation_1000.csv: Validation set of 1,000 questions, includes validation results from Heuristic approach (predicted patterns and corresponding predicted label)
(4) Pattern_code_list.csv (pattern code from Pattern Catalog) is a utility file for Heuristic approach
(5) issue.csv (1000 questions from validation set) is a utility file for Heuristic approach and LLM
(6) sub-folder prompt: contains required system message and example for the CoT prompt used by GPT models

## 2 Implementation Summary
In folder "code/", files should be:
(1) Hueristic_NLP.zip: Implementation for the heuristic approach, requirement: Stanford CoreNLP toolkit, configured with Maven setup in Java within the IntelliJ IDEA platform
(2) SVM.ipynb: Implementation for the SVM approach, requirement: scikit-learn package installed, detail instructions included in the jupytern notebook
(3) Pretrained_Detection.ipynb: Implementation for the pre-trained models, requirements: tensorflow2 with GPU, detail instructions included in the jupytern notebook
(4) Pretrained_withPattern_Detection.ipynb: Implementation for the pre-trained models with patterns featured added, detail instructions included in the jupytern notebook
(5) OpenAI_Detect.ipynb: Implementation for GPT-3.5 Turbo and GPT_4o, requirements: OpenAI package installed, detail instructions included in the jupytern notebook

## 3 Experimental Results Summary
In folder "experiment/", subfolders should be:
(1) svm: validation results as shown in Table 4 in the paper
(2) pretrained: validation results as shown in Table 4 in the paper
(3) OpenAI: validation results as shown in Table 5 and 7 in the paper
