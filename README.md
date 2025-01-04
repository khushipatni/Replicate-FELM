# Replication of FELM

FELM is a meta-benchmark designed to assess the accuracy of factual evaluations in large language models. It includes 847 questions across five key domains: world knowledge, science/technology, writing/recommendation, reasoning, and math. These questions are sourced from a variety of places, including established datasets like TruthfulQA, online platforms such as GitHub repositories, ChatGPT-generated prompts, and drafts provided by the authors.

## Download dataset

  ```
  wget https://huggingface.co/datasets/hkust-nlp/felm/resolve/main/all.jsonl
  ```


## Data Description
#### Dataset Snapshot

Category | Data
--- | ---
Number of Instances | 847
Number of Fields | 5
Labeled Classes | 2
Number of Labels | 4427

#### Descriptive Statistics


Statistic | All | world_knowledge | Reasoning | Math | Science/tech | Writting/Recommendation 
--- | --- | --- | --- | --- | --- | ---
Segments | 4427 | 532  | 1025 | 599 | 683 |  1588
Positive segments | 3642 | 385  | 877 | 477 | 582 |1321 
Negative segments |785 | 147  | 148 | 122 | 101 | 267  

#### Data Fields

| Field Name  | Field Value | Description                                 |
| ----------- | ----------- | ------------------------------------------- |
| index         | Integer     | the order number of the data point          |
| source   | string      | the prompt source   |
| prompt           | string      | the prompt for generating response                   |
| response           | string      | the response of ChatGPT for prompt                  |
| segmented_response           | list      | segments of reponse                   |
| labels          | list      | factuality labels for segmented_response                  |
| comment      | list      | error reasons for segments with factual error  |
| type | list      |  error types for segments with factual error        |
| ref | list      |  reference links       |


#### A Data Point


```
{"index": "0", 
 "source": "quora", 
 "prompt": "Which country or city has the maximum number of nuclear power plants?", 
 "response": "The United States has the highest number of nuclear power plants in the world, with 94 operating reactors. Other countries with a significant number of nuclear power plants include France, China, Russia, and South Korea.",
 "segmented_response": ["The United States has the highest number of nuclear power plants in the world, with 94 operating reactors.", "Other countries with a significant number of nuclear power plants include France, China, Russia, and South Korea."], 
 "labels": [false, true],
 "comment": ["As of December 2022, there were 92 operable nuclear power reactors in the United States.", ""], 
 "type": ["knowledge_error", null], 
 "ref": ["https://www.eia.gov/tools/faqs/faq.php?id=207&t=3"]}

```
#### Environment

System Requirements  
- **Python Version:** Python 3.10  
- **Rust Compiler:**  
  Install Rust using:  
  ```
  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh  
  ```

Install the required dependencies:
```
pip install -r requirements.txt 
```

#### Evaluation on FELM

To reproduce the results:
```
cd eval
#put "all.jsonl" here (Downloaded by Method 1)
bash eval.sh
#You can choose "vicuna_7B", "vicuna_30B", "gpt-3.5-turbo" and "gpt-4" for the parameter "model".
#You can choose "raw", "cot", "link", "content" and "cot-cons"(cot-cons means cot self-consistency method) for the parameter "method".
#replace 'Your OPENAI KEY' with your openai api key if using GPT-3.5 or GPT-4
```


## Licenses

[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)

This work is licensed under a [MIT License](https://lbesson.mit-license.org/).

[![CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](http://creativecommons.org/licenses/by-nc-sa/4.0/)

The FELM dataset is licensed under a
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-nc-sa/4.0/).

## Citation

```bibtex
@inproceedings{
chen2023felm,
title={FELM: Benchmarking Factuality Evaluation of Large Language Models},
author={Chen, Shiqi and Zhao, Yiran and Zhang, Jinghan and Chern, I-Chun and Gao, Siyang and Liu, Pengfei and He, Junxian},
booktitle={Thirty-seventh Conference on Neural Information Processing Systems Datasets and Benchmarks Track},
year={2023},
url={http://arxiv.org/abs/2310.00741}
}

```



