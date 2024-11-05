# FaiRLLM

The code for "Is ChatGPT Fair for Recommendation? Evaluating Fairness in Large Language Model Recommendation"
Here is our FaiRLLM benchmark.

> **Disclaimer**: I am not the author of this code or affiliated with the authors of the research paper. This repository is a fork intended for personal use and adaptation, and I have made updates to certain parts of the code to align with a new release. If you use this code, please refer to the original authors for proper acknowledgment.

## Prerequisites

### 1. Environment Variables

To run the code, set up the following environment variables in a `.env` file in the root directory. This file stores your Azure OpenAI API credentials:

```
AZURE_OPENAI_API_KEY = "your_api_key_here"
AZURE_OPENAI_ENDPOINT = "https://<your-resource-name>.openai.azure.com/"
AZURE_OPENAI_API_VERSION = "your_api_version"
```

Replace your_api_key_here, <your-resource-name>, and your_api_version with your actual Azure OpenAI information.

> **Add .env to your .gitignore**

### 2. Dependencies

Install required Python packages:

```
pip install pandas argparse tqdm backoff openai python-dotenv
```

### 3. Running the Benchmark

You can run the recommendation benchmark using either run_music.sh for music recommendations or run_movie.sh for movie recommendations. Each script iterates over different sensitive attribute classes (like country, age, gender) and retrieves recommendations based on the specified parameters.

### Example Usage

An example of running run_movie.sh:

```
for recommend_num in 20
do
    for sst in country neutral
    do
        echo $sst
        python3 -u ./movie/run.py \
        --director_list ./movie/director.csv \
        --sst_class $sst \
        --recommend_num $recommend_num \
        --save_folder ./movie/top_${recommend_num}/${sst}/ \
        --sst_json_path ./sst_json.json
    done
done
```

### Sensitive Attributes

The sst parameter defines the sensitive attribute to evaluate fairness. It can be set to various categories such as age, country, gender, continent, occupation, race, religion, or physics. Setting sst to neutral results in neutral recommendations, which are essential for evaluating fairness.

## 4. Data Processing

After running the benchmark, use the process.ipynb Jupyter notebook to evaluate fairness based on the collected data.

Open process.ipynb.

Set the paths at the beginning of the notebook:

```
# Input the sensitive attribute JSON path
sst_path = "./sst_json.json"  # CHANGE ME

# Input the path to the LLM result files, e.g., "./movie"
result_path = "./movie"  # CHANGE ME
```

## Data Source Acknowledgment

Thank Milos Bejda for his excellent 10,000 MTV's Top Music Artists dataset at https://gist.github.com/mbejda/9912f7a366c62c1f296c!

Please kindly cite our paper if you use our code/dataset.

```
@article{zhang2023chatgpt,
title={Is ChatGPT Fair for Recommendation? Evaluating Fairness in Large Language Model Recommendation},
author={Zhang, Jizhi and Bao, Keqin and Zhang, Yang and Wang, Wenjie and Feng, Fuli and He, Xiangnan},
journal={arXiv preprint arXiv:2305.07609},
year={2023}
}
```
