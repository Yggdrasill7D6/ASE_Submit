# ASE_Submit
Automatically assess the quality of the questions in developer chatrooms by detecting missing information (ETD and PS)

## 1 Dataset Summary
In folder "data/", files should be: 
- Pattern_Catalog_66.xlsx: Pattern Catelog of 66 lexico-syntactic patterns based on 1000 questions in the pattern discovery set
- PatternDiscovery_1000.csv:  Pattern discovery set of 1,000 questions, artifacts from open coding procedure, including maunally identified sentences containing ETD/PS, pattern_code of summarized patterns, labels
- Validation_1000.csv: Validation set of 1,000 questions, validation results from Heuristic approach, including predicted patterns and corresponding predicted label
- Pattern_code_list.csv (pattern code from Pattern Catalog) is a utility file for Heuristic approach
- issue.csv (1000 questions from validation set) is a utility file for Heuristic approach and LLM
- tag_dict.csv is a utility file for preprocessing, part of N-gram extraction process, used by SVM approach
- sub-folder prompt: contains required system message and example for the CoT prompt used by GPT models

## 2 Implementation Summary
In folder "code/", files should be:
- Hueristic_NLP.zip: Implementation for the heuristic approach, requirements: Stanford CoreNLP toolkit, configured with Maven setup in Java within the IntelliJ IDEA platform
- SVM.ipynb: Implementation for the SVM approach, requirements: scikit-learn package installed, detail instructions included in the jupyter notebook
- Pretrained_Detection.ipynb: Implementation for the pre-trained models, requirements: tensorflow2 with GPU, detail instructions included in the jupyter notebook
- Pretrained_withPattern_Detection.ipynb: Implementation for the pre-trained models with pattern features added, detail instructions included in the jupyter notebook
- OpenAI_Detect.ipynb: Implementation for GPT-3.5 Turbo and GPT_4o, requirements: OpenAI package installed, detail instructions included in the jupyter notebook

## 3 Experimental Results Summary
In folder "experiment/", subfolders should be:
- svm: validation results as shown in Table 4 in the paper
- pretrained: validation results as shown in Table 4 in the paper
- OpenAI: validation results as shown in Table 5 and 7 in the paper
