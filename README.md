<h1 align="center">
FineSumFact
</h1>


<h3 align="center">
Learning to Verify Summary Facts with Fine-Grained LLM Feedback
</h3>



<div align="center">
  <p>Authors: Jihwan Oh, Jeonghwan Choi, Nicole Hee-Yeon Kim, Taewon Yun, Hwanjun Song</p>

<p align="center">
  <img src="FineSumFact_main.png" alt="" width="500">
</p>

</div>

## Highlight
**FineSumFact** is a large-scale dataset for training language models, containing fine-grained factual feedback on summaries. It contains 100k+ document-summary feedbacks with reason and error category. The summaries are generated by 10 distinct LLMs, and feedback is produced by Llama-3-70B-Instruct. Additionally, we provide 6k+ document-summary pairs with binary feedback, aggregated from 4 existing human-labeled datasets. 

Here is our paper on arXiv: [[link](https://arxiv.org/abs/2412.10689)]\
If you are interested in our dataset, please contact here: jh.oh@kaist.ac.kr
<br/> 

## LLM feedback
We build a large-scale dataset with LLM feedback to train a fact verifier. Our dataset
contains 10,877 documents with 7 domains: CNN/DM, MediaSum, DialogSum, MeetingBank, WikiHow, GovReport, and PubMed. These source documents are used to construct labeled data with LLM feedback to train our fact verification model, following these two steps:

**(1) Summary Generation**: We generate summaries using 10 different LLMs to ensure a diverse distribution of summaries that include various types of fact errors. The summaries are generated by non-LLMs (BART-large-cnn, FLAN-T5-
large, Pegasus-Large), open-source LLMs (Phi-2,
Llama-2-13B-chat, Mistral-7B-Instruct, Mixtral7B-Instruct), and commercial LLMs (ClaudeInstant, GPT-3.5-turbo, GPT-4-turbo).

**(2) Feedback Generation**: Ensuring high-quality feedback for fact-checking is essential. Hence, we adopt an off-the-shelf LLM-based fact verifier [FineSurE](https://aclanthology.org/2024.acl-long.51/), which produces fact error types and provides reasoning for the decisions. We use Llama-3-70B-Instruct as the backbone of FineSure since it exhibited the bestbalanced accuracy of 92.0% in the sentence-level fact check. We acquire the feedback on nine fact error
categories along with the reasoning behind the decision, including “no error" (NoE), “out of context error" (OutE), “entity error" (EntE), “predicate error" (PredE), “circumstantial error" (CirE), “grammatical error" (GramE), “linking error"(LinkE), “corefernce error" (CorefE), and “other error" by [FRANK](https://aclanthology.org/2021.naacl-main.383/). As a result, we collect LLM feedback on 102,640 document-summary pairs as the training data.


| Field               | Description                                |
|---------------------|--------------------------------------------|
| id                  | Data unique ID                             |
| doc_id              | ID in source dataset                       |
| source              | Source dataset name                        |
| split               | Trainset                                   |
| model_summary       | Summary text generated by LLM (list of sentences)       |
| summarizer          | Summarizer name                            |
| document            | Document text                              |
| cnt_llama3_tokens   | Document lenght                            |
| llm_output          | Raw output of fine-grained feedback (before JSON parsing) |
| pred_factual_labels | List of binary labels for each sentence  (0: factually correct, 1: otherwise)|

<br/> 

## Human feedback
We aggregate all the available human-labeled datasets for sentence-level fact verification, including [AggreFact](https://aclanthology.org/2023.acl-long.650/), [DiaSumFact](https://aclanthology.org/2023.acl-long.377/), [TofuEval](https://aclanthology.org/2024.naacl-long.251/), and [Ramprasad'24](https://aclanthology.org/2024.eacl-short.7/). The aggregated data contains 6,546 document-summary pairs, each of which has sentence-level binary labels – “0" for no error and “1" for a fact error. 5,853 feedbacks are used for training set, 693 feedbacks are used for test set.

| Field               | Description                                |
|---------------------|--------------------------------------------|
| id                  | Data unique ID                             |
| doc                 | Document text                              |
| model_summary       | Summary text                               |
| label               | List of binary labels for each sentence  (0: factually correct, 1: otherwise)|
| source              | Source dataset name                        |
<br/> 

## Citation

Please consider citation if our paper is useful in your research.
```BibTeX
TBD
```

###### *This work was done @ KAIST Data Intelligence System Lab*
