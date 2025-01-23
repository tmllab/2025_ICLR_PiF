<div align="center">

# Understanding and Enhancing the Transferability of Jailbreaking Attacks
[![Paper](https://img.shields.io/badge/paper-ICLR-green)]()

</div>

Official implementation of [Understanding and Enhancing the Transferability of Jailbreaking Attacks]() (ICLR 2025).

## Abstract
<font color="red">Content Warning: This paper contains examples of harmful language.</font>

Jailbreaking attacks can effectively manipulate open-source large language models (LLMs) to produce harmful responses.
However, these attacks exhibit limited transferability, failing to disrupt proprietary LLMs consistently.
To reliably identify vulnerabilities in proprietary LLMs, this work investigates the transferability of jailbreaking attacks by analyzing their impact on the model's intent perception.
By incorporating adversarial sequences, these attacks can redirect the source LLM's focus away from malicious-intent tokens in the original input, thereby obstructing the model's intent recognition and eliciting harmful responses.
Nevertheless, these adversarial sequences fail to mislead the target LLM's intent perception, allowing the target LLM to refocus on malicious-intent tokens and abstain from responding.
Our analysis further reveals the inherent $\textit{distributional dependency}$ within the generated adversarial sequences, whose effectiveness stems from overfitting the source LLM's parameters, resulting in limited transferability to target LLMs.
To this end, we propose the Perceived-importance Flatten (PiF) method, which uniformly disperses the model's focus across neutral-intent tokens in the original input, thus obscuring malicious-intent tokens without relying on overfitted adversarial sequences.
Extensive experiments demonstrate that PiF provides an effective and efficient red-teaming evaluation for proprietary LLMs.
<p float="left" align="center">
<img src="Method.pdf" width="650" />

**Figure.** A conceptual diagram of the classifier’s decision boundary and training samples. The training samples belonging to NAE (blue) can effectively mislead the classifier, while AAE (red) cannot. The left panel shows the decision boundary before optimizing AAEs, which only has a slight distortion. The middle panel shows the decision boundary after optimizing AAEs, which exacerbates the distortion and generates more AAEs.
</p>

## Requirements
- This codebase is written for `python3` and 'pytorch'.
- To install necessary python packages, run `pip install -r requirements.txt`.


## Experiments
### Data
- Please download and place all datasets into the data directory.


### Training


Generate jailbreaking attack based on MLM (Bert)

```
python3 PiF_MLM.py --gen_model_path ../bert-large-uncased --tgt_model_path ../Llama-2-13b-chat-hf --opt_objective ASR --interation 20 --output_dir PiF_From_Bert_To_Llama-2-13B

```

Generate jailbreaking attack based on CLM (Llama)

```
python3 PiF_CLM.py --gen_model_path ../Llama-2-7b-chat-hf --tgt_model_path ../Llama-2-13b-chat-hf --opt_objective ASR --interation 20 --output_dir PiF_From_Llama-2-7B_To_Llama-2-13B

```

Jailbreaking GPT evaluated by keyword ASR

```
python3 PiF_MLM.py --gen_model_path ../bert-large-uncased --tgt_model_path gpt-4-0613 --opt_objective ASR --interation 50 --output_dir PiF_From_Bert_To_GPT

```

Jailbreaking GPT evaluated by keyword ASR+GPT

```
python3 PiF_MLM.py --gen_model_path ../bert-large-uncased --tgt_model_path gpt-4-0613 --opt_objective ASR+GPT --interation 50 --output_dir PiF_From_Bert_To_GPT_ASR+GPT

```

## License and Contributing
- This README is formatted based on [paperswithcode](https://github.com/paperswithcode/releasing-research-code).
- Feel free to post issues via Github.

## Reference
If you find the code useful in your research, please consider citing our paper:

<pre>

</pre>
