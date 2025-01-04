# Replication of FELM

 FELM is a meta benchmark to *evaluate factuality evaluation* for large language models.
 The benchmark comprises 847 questions that span five distinct domains: world knowledge, science/technology, writing/recommendation, reasoning, and math. We gather prompts corresponding to each domain by various sources including standard datasets like truthfulQA, online platforms like Github repositories, ChatGPT generation or drafted by authors.

 We then obtain responses from ChatGPT for these prompts. For each response, we employ fine-grained annotation at the segment level, which includes reference links, identified error types, and the reasons behind these errors as provided by our annotators.

## Download

- Download the whole dataset by:
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


#### Typical Data Point


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
#### Evaluation on FELM

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

To reproduce our results:
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

Please cite our paper if you use our dataset:
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



