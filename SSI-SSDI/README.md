# The performance of different approaches on SSI/SSDI
Conclusion: `AdvancedRAG` (We used [PaperQA implementation](https://github.com/Future-House/paper-qa)) seem to be the best in `NaiveRAG`, `GraphRAG` and `Logic LLM (with RAG)`.

## Basic test cases (F1 score)
|Approach               |F1 score    |
|-----------------------|------------|
|Policy Engine          |0.4473684211|
|Perplexity.ai(baseline)|0.9827586207|
|NaiveRAG               |0.8793103448|
|AdvancedRAG            |0.8965517241|
|GraphRAG               |0.6551724138|
|Logic LLM              |0.8793103448|

## Scenario test cases (ROUGE score)
|Approach   |rouge1             |rouge2              |rougeL             |rougeLsum          |
|-----------|-------------------|--------------------|-------------------|-------------------|
|NaiveRAG   |0.10638972974600375|0.03332123277906021 |0.07092772930309406|0.09179419033228833|
|AdvancedRAG|0.22694791192729363|0.0610002691993031  |0.14573577658754394|0.14553024242745344|
|GraphRAG   |0.1262765092746989 |0.033861502970296505|0.08621287227334787|0.10267322829949359|
|Logic LLM  |0.09550044274878426|0.018672250657445558|0.06790505095745589|0.08147286797283657|

# Approaches
Would be great if we can also add `RAPTOR` and other approaches.

## Perplexity.ai
The baseline LLM [solution with web search integrated](https://perplexity.ai).

## PolicyEngine
The [expert system coded by human](https://github.com/PolicyEngine).

> ℹ️ PolicyEngine produced 100% correct answer if we do not count `not sure` cases as wrong answer.
## Naive RAG
Basic RAG, question is used to query vector storage of POMS document and get top 25 chunks to be used as a part of context for LLM to answer the question. {arxiv:2312.10997}
## AdvancedRAG
We used [PaperQA implementation](https://github.com/Future-House/paper-qa). {arXiv:2312.07559}
## GraphRAG
We used [Microsoft GraphRAG implementation](https://github.com/microsoft/graphrag). {arXiv:2404.16130}
## Logic LLM with RAG
We added RAG for [Logic-LLM](https://github.com/teacherpeterpan/Logic-LLM). {arXiv:2305.12295}  
Or say We added Prolog and RAG for [Program of Thoughts](https://github.com/TIGER-AI-Lab/Program-of-Thoughts). {arxiv:2211.12588}

# Test method
Single round Q&A, compare to human response.

* Metric 1 compare if prediction and target in same category `yes`, `no` (we allow predict of `not sure`).
* Metric 2 `ROUGE`.

> ⚠️ It is important to know that we count all `not sure` as wrong answer.

# Test dataset
- Knowledge input: [POMS document](doc.md)
- Questions and target answers:
  - [test-cases.jsonl](test-cases.jsonl)
  - [scenario-test-cases.jsonl](scenario-test-cases.jsonl)

> 💡 For `test-cases.jsonl`, add prompt `Answer the question with yes or no.` before question will simplify the benchmark task.

# Citation
```
@misc{georgetown_mdi_beeck_ssi_ssdi_2024,
  author = {Raifman, Marc and Burka, Nicholas and Xu, Yuan},
  title = {SSI-SSDI Dataset},
  howpublished = {\url{https://github.com/Georgetown-MDI-Beeck-Collaboration/p2c2024-team-collection/tree/main/SSI-SSDI}},
  year = {2024},
  organization = {Georgetown MDI Beeck Collaboration}
}
```
