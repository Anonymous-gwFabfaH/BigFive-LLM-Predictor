# Predicting the Big Five Personality Traits in Chinese Counselling Dialogues Using Large Language Models

This repository contains the code and instructions for the paper "Predicting the Big Five Personality Traits in Chinese Counselling Dialogues Using Large Language Models".

## Abstract
Accurate assessment of personality traits is crucial for effective psycho-counseling, yet traditional methods like self-report questionnaires are time-consuming and biased. This study examines whether Large Language Models (LLMs) can predict the Big Five personality traits directly from counseling dialogues and introduces an innovative framework to perform the task. Our framework applies role-play and questionnaire-based prompting to condition LLMs on counseling sessions, simulating client responses to the Big Five Inventory. We evaluated our framework on 853 real-world counseling sessions, finding a significant correlation between LLM-predicted and actual Big Five traits, proving the framework's validity. Moreover, ablation studies highlight the importance of role-play simulations and task simplification via questionnaires in enhancing prediction accuracy. Our fine-tuned Llama3-8B model, utilizing Direct Preference Optimization with Supervised Fine-Tuning, achieves a 130.95% improvement, surpassing the state-of-the-art Qwen1.5-110B by 36.94% in personality prediction validity. In conclusion, LLMs can predict personality based on counseling dialogues. Our code and model are publicly available at [GitHub](https://github.com/Anonymous-gwFabfaH/BigFive-LLM-Predictor), providing a valuable tool for future research in computational psychometrics.

## File Structure
- `generate_bfi_requests.py` - Generates Big Five Inventory (BFI) requests for the counseling dialogues following our role-play and questionnaire-based prompting framework.
- `process_results.py` - Processes the results of the LLM predictions and calculates the OCEAN scores.

*Note: The generated requests can be processed with [api_request_parallel_processor.py](https://github.com/openai/openai-cookbook/blob/main/examples/api_request_parallel_processor.py) from the OpenAI Cookbook.*

## Data Schema
Each counseling dialogue session is stored in a separate TXT file. Each utterance has a prefix indicating the speaker, either "咨询师" (Counselor) or "来访者" (Client). The dialogues are in Chinese.

Each file is named using the format `{Client_ID}_chat_{Chatround_ID}_{Timestamp}.txt`, where:
- `Client_ID` is the unique identifier of the client.
- `Chatround_ID` is the number of chat rounds in the counseling session.
- `Timestamp` is the timestamp of the counseling session.

## Model Checkpoints
The model checkpoints are available at [Hugging Face Model Hub](https://huggingface.co/loeol/Llama-3-8b-BFI-Anonymous).

Based on [`meta-llama/Meta-Llama-3-8B`](https://huggingface.co/meta-llama/Meta-Llama-3-8B), you can use `transformers` from Hugging Face or `vLLM` to load and serve the model.

## Getting Started
To get started, clone the repository and install the necessary dependencies:
```bash
git clone https://github.com/Anonymous-gwFabfaH/BigFive-LLM-Predictor.git
cd BigFive-LLM-Predictor
pip install -r requirements.txt
```

### Generating BFI Requests
To generate the Big Five Inventory requests for your counseling dialogues, run:
```bash
python generate_bfi_requests.py --model_name MODEL_NAME --source_path path_to_your_dialogues --output_path path_to_output_requests
```

### Processing Results
To process the results of the LLM predictions and calculate the OCEAN scores, run:
```bash
python process_results.py
```
Note: modify the `process_results.py` script to load the LLM predictions and define the output path for the OCEAN scores.

