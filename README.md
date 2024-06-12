# ASE_Submit
This is a replication package for "Detecting Missing Information of Questions in Q&A Chatrooms".

Goal: Automatically assess the quality of the questions in developer chatrooms by detecting missing information (ETD and PS)
- Problem Statement (PS) — A summary of the program's malfunction or any problematic scenario currently encountered by the user.
- Expect to Do (ETD) — A summary outlining the anticipated behavior of the program or other expectations from the user.

## 1 File Structure
In folder "data/": 
- Pattern_Catalog_66.xlsx: Pattern Catelog of 66 lexico-syntactic patterns based on 1000 questions in the pattern discovery set
- PatternDiscovery_1000.csv:  Pattern discovery set of 1,000 questions, artifacts from open coding procedure, including maunally identified sentences containing ETD/PS, pattern_code of summarized patterns, labels
- Validation_1000.csv: Validation set of 1,000 questions, validation results from Heuristic approach, including predicted patterns and corresponding predicted label
- Pattern_code_list.csv (pattern code from Pattern Catalog) is a utility file for Heuristic approach
- issue.csv (1000 questions from validation set) is a utility file for Heuristic approach and LLM
- tag_dict.csv is a utility file for preprocessing, part of N-gram extraction process, used by SVM approach
- sub-folder prompt: contains required system message and example for the CoT prompt used by GPT models

In folder "code/":
- Hueristic_NLP.zip: Implementation for the heuristic approach
- SVM.ipynb: Implementation for the SVM approach, requirements: scikit-learn package installed, detail instructions included in the jupyter notebook
- Pretrained_Detection.ipynb: Implementation for the pre-trained models, requirements: tensorflow2 with GPU, detail instructions included in the jupyter notebook
- Pretrained_withPattern_Detection.ipynb: Implementation for the pre-trained models with pattern features added, detail instructions included in the jupyter notebook
- OpenAI_Detect.ipynb: Implementation for GPT-3.5 Turbo and GPT-4o, requirements: OpenAI package installed, detail instructions included in the jupyter notebook

In folder "experiment/":
- svm: validation results as shown in Table 4 in the paper
- pretrained: validation results as shown in Table 4 in the paper
- OpenAI: validation results as shown in Table 5 and 7 in the paper

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
To replicate Heuristic approach:
- Environment requirements: Stanford CoreNLP toolkit, configured with Maven setup in Java within the IntelliJ IDEA platform
- Input Files: "issue.csv" and "Pattern_code_list.csv" in folder "data/"
- Steps to reproduce: Unzip the file "Hueristic_NLP.zip" and import this project into IntelliJ

To replicate SVM approach:
