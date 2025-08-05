Great. I’ll conduct a comprehensive review of how LLMs have been applied to the BioASQ-QA challenge over the past 5 years, across all task types (factoid, list, yes/no, and summary). This will include peer-reviewed publications, preprints, blog posts, and GitHub repositories.

I'll also investigate whether any researchers have adopted agentic or multistep LLM systems for BioASQ-QA and analyze the advantages and disadvantages of such an approach.

I'll let you know when the findings are ready.


# Large Language Models for BioASQ Biomedical QA (2018–2025)

## Background: BioASQ Challenges and QA Tasks

BioASQ is an annual challenge on biomedical semantic indexing and question answering. The **BioASQ Task B** focuses on **Biomedical QA**, with question types including *yes/no*, *factoid*, *list*, and *summary (ideal)* answers. Systems typically first retrieve relevant articles/snippets (Phase A) and then produce answers (Phase B). Over the past five years, the field has shifted from traditional IR+NLP pipelines to **transformer-based large language models (LLMs)** specialized for biomedical text. Below, we review how LLM-based approaches have tackled BioASQ QA, and then discuss the merits and drawbacks of a more *agentic* (multi-step or tool-using) LLM approach in this domain.

## Transformer Era: BERT and Domain-Specific Models in BioASQ

The introduction of **BERT** (2018) and its domain adaptations revolutionized BioASQ systems. **BioBERT** (Lee et al. 2019), a BERT pre-trained on biomedical literature, showed large gains on QA and was **widely adopted by the majority of teams in BioASQ7 and BioASQ8 (2019–2020)**. For example, BioBERT helped improve factoid and list answer extraction by better understanding biomedical terminology.

By BioASQ9 (2021), teams had expanded to other state-of-the-art transformers: *RoBERTa, ALBERT, ELECTRA, and XLNet* were all explored. Many top systems fine-tuned such models on BioASQ training QA pairs. Participants also began creating **Biomedical Transformer variants** pre-trained on PubMed and other corpora. Notably:

* **PubMedBERT** (Gu et al. 2020) – a BERT trained from scratch on PubMed – improved BioASQ 7 factoid and yes/no accuracy, especially on questions requiring up-to-date domain knowledge. A larger “PubMedBERT-large” further boosted performance on yes/no questions.
* **BioMegatron, BioRoBERTa** (2021) – large biomedical language models (some with 345M+ parameters) – examined effects of bigger model size and vocab on BioASQ. These models, along with **BlueBERT** (clinical BERT), continued to push incremental gains.
* **BioLinkBERT** (2022) – introduced a novel pre-training objective using citation links to imbue a model with biomedical relational knowledge. BioLinkBERT achieved new SOTA on BioASQ7b yes/no questions, outperforming PubMedBERT on that task.

Crucially, these domain-specific LMs reduced the gap between general LMs and biomedical expert knowledge. **Most BioASQ systems through 2022 used a transformer reader model (e.g. BioBERT or a variant) to extract answers from retrieved snippets**. For yes/no questions, teams often framed it as text classification with a BERT-based classifier. For factoids and list questions, a common approach was to fine-tune models in a **reading comprehension format** (SQuAD-style span extraction). In fact, the BioBERT team introduced a method to convert list questions into a SQuAD-style QA format back in BioASQ7, treating list answers as multiple spans in a context. This helped transformer models handle list-type questions by finding all relevant answer entities in text.

**Example:** One BioASQ10 (2022) system from Macquarie University used a *DistilBERT*-based classifier to score candidate answer sentences for summary questions. They retrieved documents and snippets, then ranked sentences by relevance using *sBERT* embeddings, and finally returned the top-scoring sentences as a concise “ideal answer”. This extractive summarization approach – essentially a BERT sentence selection – illustrates how even multi-sentence answers were tackled with smaller transformers. Other teams merged data from previous BioASQ years to counter training set sparsity. For instance, one BioASQ10 participant merged factoid and list question data to augment training; this yielded a **20% boost on list questions and perfect scores on some yes/no batches** after careful hyperparameter tuning. Overall, by 2022, **powerful but task-specific models (BioBERT, BioELECTRA, etc.) dominated BioASQ QA**, delivering solid results with fine-tuning and clever data reuse.

## Generative LLMs (2023): GPT-3/4 and Multi-Step Reasoning

The emergence of large-scale generative LLMs like **GPT-3 and GPT-4** in 2022–2023 prompted new approaches to BioASQ. Instead of training a model for each answer type, researchers began to **prompt** large general models with biomedical questions. These models, with 100B+ parameters and broad knowledge, could potentially generate answers directly. Key developments include:

* **Zero-shot/few-shot prompting:** Early experiments with GPT-3 (175B) showed it can answer BioASQ-style questions reasonably with the right prompt, but might falter on detailed biomedical facts. However, by 2023 GPT-3.5 and GPT-4 had improved factual accuracy. Teams started exploring prompt engineering to coax reliable answers from these models.

* **BioASQ11 (2023) – GPT-4 outperforms fine-tuned models:** A notable entrant was *NCU-IISR (Taiwan)*, who used **GPT-4 via OpenAI’s API with carefully designed prompts**. They report that *“the standalone GPT-4 method”* with optimized prompts **significantly outperformed their previous BERT-based system**, achieving the highest scores in one of the BioASQ11 test batches. In fact, they attempted a hybrid (feeding GPT-4 outputs into their 2022 BERT+BERTScore system), but GPT-4 alone was **much better**. This demonstrates the raw power of modern LLMs: GPT-4, even without domain-specific fine-tuning or external knowledge, was able to produce accurate answers for many questions, likely leveraging the vast biomedical data in its pretraining.

* **Challenges:** Despite this success, generative LLMs can **hallucinate** facts and have knowledge cutoffs (e.g. GPT-4’s knowledge is mostly up to 2021). In BioASQ, where correctness is paramount, uncontrolled generation is risky. For example, a factoid answer must exactly match a specific biomedical entity – an LLM might give a plausible but incorrect gene name or drug. Thus, 2023 systems began to **combine LLMs with retrieval** to ground answers in evidence. Large models like ChatGPT were used in a Retrieval-Augmented Generation (RAG) setup: first fetch relevant snippets from PubMed, then prompt the LLM with those snippets plus the question so it generates a supported answer.

* **MIRAGE/MedRAG benchmark:** Very recently, researchers introduced **MIRAGE**, a benchmark of 7,600 medical questions (including BioASQ data), to systematically evaluate retrieval-augmented LLMs. Using their **MedRAG** pipeline, they compared 41 combinations of retrievers, knowledge corpora, and LLMs. A key finding was that **augmenting LLMs with retrieved biomedical texts boosts accuracy by up to 18% compared to prompting alone (chain-of-thought)**. In other words, an LLM like GPT-3.5 or a fine-tuned LLaMA-2 performs much better when it can **quote PubMed articles** rather than relying purely on parametric memory. This result aligns with the community’s shift toward *tool-using LLMs* for biomedical QA.

In summary, by 2023 we see two successful paradigms: (1) using a **powerful LLM (GPT-4)** directly with sophisticated prompting, and (2) using **medium-sized biomedical LMs with retrieval** (a multi-step RAG approach). Both outperform the older single-step fine-tuned models on various BioASQ tasks. This naturally leads to the idea of an *agentic LLM system* – i.e. an LLM that actively orchestrates multiple tools or steps – to tackle biomedical QA more robustly.

## Toward Agentic LLM Systems in Bio Research

An **agentic LLM** is one that doesn’t just answer in one go, but can **plan actions, call external tools (e.g. search engines, databases), and reason in multiple steps** to arrive at an answer. In bioinformatics and biomedical QA, an agentic approach might involve the LLM breaking a complex question into sub-questions, retrieving literature for each, consulting domain knowledge bases (like UMLS or MeSH), and then composing the final answer with justification. This is inspired by how a human expert might research: ask clarification questions, read papers, and aggregate findings.

**Has this been tried for BioASQ?** Yes – at least in research settings. A recent example is **Discuss-RAG (2025)** by Xuanzhao Dong et al., which specifically targets medical QA (including BioASQ) with a multi-agent framework. Their system employs a **“team of LLM-based medical experts”** that engage in a multi-turn *discussion* overseen by a *summarizer agent*, mimicking a brainstorming session. Another *decision agent* then evaluates the candidate answers/snippets before final answer formulation. By modeling human-like reasoning and debate among specialized agents, Discuss-RAG achieved a **significant accuracy boost – up to +16.7% in BioASQ answer accuracy** – over a standard retrieval-augmented baseline. This is a striking validation of agentic reasoning: the LLM agents collaboratively refine relevant knowledge and correct each other’s mistakes, addressing two common issues in LLM QA: hallucinations and irrelevant context.

Outside of official BioASQ entries, the literature shows growing interest in agentic LLMs for biomedicine. For instance, one 2025 system called **LLM-Enhancer** connects an LLM to multiple online sources (Google Search, Wikipedia, DuckDuckGo, etc.) via custom agent tools. It uses vector embeddings to fetch the *most pertinent facts* and feeds those into the LLM during dialogue, which **greatly reduces hallucinations while preserving answer fluency**. In essence, the LLM learns to delegate knowledge lookup to external tools – a hallmark of an agentic approach. Similarly, the general idea of “self-ask with search” (where the LLM iteratively formulates search queries to answer a question) could be applied to biomedical QA to break down multi-faceted questions.

## Advantages of an Agentic Approach

Using an agentic LLM system for BioASQ-style QA offers several **key advantages**:

* **Incorporation of External Knowledge:** An agentic LLM can query up-to-date biomedical databases and literature in real time. This mitigates the **“outdated knowledge” problem of static models**, ensuring answers reflect the latest research (critical in biomedicine). It also curbs hallucinations – the LLM is prompted with actual retrieved facts, grounding its responses in reality.

* **Complex Reasoning via Decomposition:** Agent frameworks can break complex questions into manageable parts. BioASQ often asks multi-part questions (e.g. a list of causes *and* treatments for a disease). An LLM agent could generate sub-questions and solve them sequentially, improving handling of **multi-step reasoning tasks**. This approach mirrors human problem-solving and can yield more precise answers.

* **Ensemble of Specialists:** By assigning roles to different LLM agents (as Discuss-RAG did with “medical experts” vs. a “summarizer”), the system can emulate a panel of specialists. Each agent can focus on a particular aspect (e.g. one agent specializes in genetics-related questions, another in clinical trials). This specialization can improve accuracy on domain-specific details. The summarizer or a lead agent then integrates these perspectives, potentially producing a more comprehensive answer than a single monolithic model.

* **Transparency and Verification:** An agentic workflow can provide an *audit trail* of how an answer was obtained – e.g. which papers were retrieved, what intermediate conclusions were drawn. This is valuable in biomedical QA for **trustworthiness**. It’s easier to **cite sources** (important in BioASQ evaluations) when the system explicitly retrieved those snippets. The decision agent in Discuss-RAG, for example, evaluates retrieved snippets before use, which adds a layer of result verification. Such modularity allows pinpointing which component erred when a wrong answer is produced, aiding debugging and improvement.

In summary, an agentic LLM can leverage the best of both worlds: the **knowledge and reasoning ability of large LMs** and the **factual accuracy of external knowledge sources**, yielding answers that are both accurate and up-to-date.

## Disadvantages and Challenges of Agentic Systems

However, these benefits come with **trade-offs**. Some **drawbacks and challenges** of the agentic approach include:

* **System Complexity:** An agentic pipeline has many moving parts (multiple agents, tool APIs, intermediate prompts). This complexity makes the system harder to implement and maintain. There are more opportunities for errors – e.g. a retrieval agent might fetch irrelevant info that misleads the answer agent. In BioASQ’s strict evaluation setting, a single broken step can cause failures. The simplicity of a single fine-tuned model is an advantage in terms of robustness and latency.

* **Efficiency and Latency:** Multi-step reasoning is typically **slower**. Each agent-tooled step (searching literature, parsing results, asking follow-up questions) adds runtime. For example, a pipeline that calls an LLM 5 times (for planning, multiple queries, then answering) will be significantly slower than a single forward pass of a fine-tuned BERT. This may or may not be acceptable depending on the use-case, but in a competition setting or real-time clinical decision support, long delays are problematic.

* **Prompt Design and Optimization:** Agentic systems rely heavily on prompt engineering to coordinate agents (e.g. crafting the discussion prompts between expert agents in Discuss-RAG). Designing effective prompts or agent instructions is non-trivial and often task-specific. It introduces another layer of “hyperparameters” to tune (the phrasing of prompts, the rules given to agents, etc.). What’s more, LLM agents might unpredictably deviate from their intended role without carefully constrained prompts.

* **Cost:** If using large API-based models (like GPT-4) for each agent or step, the **API usage cost** can multiply. Answering one question might require several LLM calls (tool use, reasoning, final answer), which could be expensive at scale. Even with open-source LLMs, running multiple large models concurrently is computationally intensive.

* **Error Propagation:** An agentic chain is only as strong as its weakest link. If the retrieval agent fails to find the crucial paper, the answer agent cannot magically know the answer (and might hallucinate). If an agent generates a flawed intermediate reasoning, subsequent agents might build on that mistake. Ensuring resilience – e.g. with a verification or backtracking mechanism – is an active research challenge. Discuss-RAG’s decision agent partly addresses this by filtering out irrelevant or low-quality snippets, but it’s hard to guarantee no good evidence is missed or wrongly discarded.

* **Evaluation Difficulty:** When an agentic system gets an answer wrong, diagnosing *which component* was responsible can be difficult. Was it a retrieval miss, a reasoning error, or a prompting issue? This complicates the development cycle. Traditional end-to-end models can be evaluated and improved holistically (e.g. by more training data), whereas agents might require targeted fixes in different modules.

Despite these challenges, the trend – in both BioASQ and the broader QA field – is clearly toward *more sophisticated, multi-step LLM systems*. The 2025 research by Dong et al. and others demonstrates that the agentic approach can yield **substantial accuracy gains in biomedical QA tasks**, which often justify the added complexity.

## Conclusion and Outlook

**In summary, the past five years have seen BioASQ QA systems evolve from single-step models (first BioBERT, then various transformer QA models) to leveraging the power of massive LLMs and multi-step reasoning.** Early transformer-based models like BioBERT and BioELECTRA brought huge improvements to BioASQ, and remain strong baselines. But recent systems show that *agentic LLM approaches – using LLMs as reasoners, planners, and tool-users – can push performance to new heights.* Large models like GPT-4, when carefully prompt-tuned, have even outperformed domain-specialized models on BioASQ questions. And by integrating retrieval or multiple agents, these LLMs can overcome their own limitations (as evidenced by a 16–18% answer accuracy boost with collaborative reasoning and retrieval augmentation).

Going forward, we expect more **hybrid agentic systems** in biomedical QA. For example, future BioASQ entries might use an LLM to dynamically decide whether a question is simple (answerable from memory) or complex (requiring tool use), a strategy that could combine the speed of direct prompting with the accuracy of an agent when needed. Another likely direction is integrating **knowledge graphs or reasoning engines** as tools for the LLM agent – an approach that could handle BioASQ questions requiring logical inference or aggregation of multiple facts.

In conclusion, **LLMs have become central to BioASQ QA research**, and the cutting edge is moving toward systems that treat these models not just as static answerers, but as **flexible agents** that can *retrieve, reason, and collaborate* to better mimic an expert biomedical researcher. This agentic paradigm, while complex, holds great promise in pushing biomedical question answering to new levels of intelligence and reliability.

**Sources:**

* Nentidis, A. *et al.* “BioASQ at CLEF2022: The Tenth Edition of the Large-scale Biomedical Semantic Indexing and Question Answering Challenge.” (overview paper)&#x20;

* Alrowili, S. and Vijay-Shanker, K. “BioM-Transformers at BioASQ10b: Findings and Techniques.” (BioASQ 2022 participant paper – domain-adapted ALBERT/ELECTRA, data augmentation)&#x20;

* Mollá, D. *et al.* “Macquarie University at BioASQ10: Query-Focused Summarization for Biomedical QA.” (BioASQ 2022 participant paper – DistilBERT, sBERT for extractive ideal answers)&#x20;

* Hsueh, C.Y. *et al.* **“NCU-IISR: Prompt Engineering on GPT-4 for BioASQ 11b.”** (BioASQ 2023 paper – using GPT-4 via API, prompt tuning)&#x20;

* Dong, X. *et al.* **“Talk Before You Retrieve: Agent-Led Discussions for Better RAG in Medical QA (Discuss-RAG).”** *arXiv preprint 2025*. (Introduces multi-agent LLM reasoning, improves BioASQ answers by \~16% with collaborative agents)&#x20;

* Meng, Z. *et al.* “MIRAGE: Benchmarking Retrieval-Augmented Generation for Medicine.” *arXiv:2402.13178, 2024*. (Systematic evaluation of LLM + retrieval on medical QA, shows RAG boosts accuracy up to 18%)&#x20;

* Rayhan, N. *et al.* “LLM Enhancer: Reducing Hallucinations with External Knowledge.” *arXiv 2025*. (Describes an agentic tool-using LLM system combining multiple search engines and a vector DB to improve factual accuracy)&#x20;
