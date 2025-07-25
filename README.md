# BIMBA

[**🌐 Homepage**](https://sites.google.com/view/bimba-mllm) | [**📖 arXiv**](https://arxiv.org/abs/2503.09590) | [**💻 GitHub**](https://github.com/md-mohaiminul/BIMBA) | [**🤗 Model**](https://huggingface.co/mmiemon/BIMBA-LLaVA-Qwen2-7B) | [**🌟 Demo**](BIMBA-LLaVA-NeXT/demo_selective_scan_compression.ipynb)

[**BIMBA: Selective-Scan Compression for Long-Range Video Question Answering**](https://arxiv.org/abs/2503.09590)\
Md Mohaiminul Islam, Tushar Nagarajan, Huiyu Wang, Gedas Bertasius, and Lorenzo Torresani\
<span style="color:red">**Accepted by CVPR 2025**</span>

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/bimba-selective-scan-compression-for-long/zero-shot-video-question-answer-on-egoschema-1)](https://paperswithcode.com/sota/zero-shot-video-question-answer-on-egoschema-1?p=bimba-selective-scan-compression-for-long)

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/bimba-selective-scan-compression-for-long/zero-shot-video-question-answer-on-vnbench)](https://paperswithcode.com/sota/zero-shot-video-question-answer-on-vnbench?p=bimba-selective-scan-compression-for-long)

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/bimba-selective-scan-compression-for-long/video-question-answering-on-perception-test)](https://paperswithcode.com/sota/video-question-answering-on-perception-test?p=bimba-selective-scan-compression-for-long)

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/bimba-selective-scan-compression-for-long/video-question-answering-on-next-qa)](https://paperswithcode.com/sota/video-question-answering-on-next-qa?p=bimba-selective-scan-compression-for-long)

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/bimba-selective-scan-compression-for-long/zero-shot-video-question-answer-on-video-mme-1)](https://paperswithcode.com/sota/zero-shot-video-question-answer-on-video-mme-1?p=bimba-selective-scan-compression-for-long)

## 📢 Latest Updates

**Mar 20, 2025**: BIMBA-LLaVA-Qwen2-7B model weigts are released on [HuggingFace 🤗](https://huggingface.co/mmiemon/BIMBA-LLaVA-Qwen2-7B) \
**Mar 20, 2025**: Released the training and evaluation code.\
**Feb 27, 2025**: BIMBA is accepted by CVPR 2025! 🔥🔥


## BIMBA Overview

BIMBA is a multimodal large language model (MLLM) capable of efficiently processing long-range videos. Our model leverages the selective scan mechanism of [Mamba](https://arxiv.org/abs/2312.00752) to effectively select critical information from high-dimensional video and transform it into a reduced token sequence for efficient LLM processing. Extensive experiments demonstrate that BIMBA  achieves state-of-the-art accuracy on multiple long-form VQA benchmarks, including [PerceptionTest](https://arxiv.org/abs/2305.13786), [NExT-QA](https://arxiv.org/abs/2105.08276), [EgoSchema](https://arxiv.org/abs/2308.09126), [VNBench](https://arxiv.org/abs/2406.09367), [LongVideoBench](https://arxiv.org/abs/2407.15754), [Video-MME](https://arxiv.org/abs/2405.21075), and [MLVU](https://arxiv.org/abs/2406.04264). 

<img src="BIMBA-LLaVA-NeXT/assets/model.png"> 

## Installation 🔧
Please use the following commands to install the required packages:
```bash
cd BIMBA-LLaVA-NeXT
conda create --name bimba python=3.10
conda activate bimba
pip install -r requirements.txt
```
This codebase is built on [LLaVA-NeXT](https://github.com/LLaVA-VL/LLaVA-NeXT) and [mamba](https://github.com/state-spaces/mamba) codebases.

## Demo Selective-Scan Compression
We provide a [demo notebook](BIMBA-LLaVA-NeXT/demo_selective_scan_compression.ipynb) on how to use selective-scan/mamba-based token compression method for long-range videos introduced in our paper. Following this notebook, you can easily utilize this compression technique to reduce the input video tokens of your model.


## Download Model
Download the model from [HuggingFace 🤗](https://huggingface.co/mmiemon/BIMBA-LLaVA-Qwen2-7B)
```bash
cd BIMBA-LLaVA-NeXT/checkpoints
git clone https://huggingface.co/mmiemon/BIMBA-LLaVA-Qwen2-7B
```

## Model Inference
Use the following script to make inference on any video.
```python
cd BIMBA-LLaVA-NeXT
python inference.py
```

## Model Training
1. Follow the [LLaVA-NeXT](https://github.com/LLaVA-VL/LLaVA-NeXT/blob/main/docs/LLaVA_Video_1003.md) codebase to prepare the training data (e.g., [LLaVA-Video-178K](https://huggingface.co/datasets/lmms-lab/LLaVA-Video-178K)). I trained on the subset of the LLaVA-Video-178K that contains videos of 1-2m and 2-3m. 
Update the [exp_small.yaml](BIMBA-LLaVA-NeXT/scripts/video/train/exp_small.yaml) file to point to your data.
2. Follow the commands below to train BIMBA model:
```bash
cd BIMBA-LLaVA-NeXT
bash scripts/video/train/Train_BIMBA_LLaVA_Qwen2_7B.sh
```

## Evaluation

### Evaluate Single Dataset (e.g., [VideoMME](https://huggingface.co/datasets/lmms-lab/Video-MME))

1. First, download the videos from the huggingface/dataset repo and replace "path_to_video_folder" accordingly.
2. We provide the formatted json files for the evaluation datasets in the `BIMBA-LLaVA-NeXT/DATAS/eval` folder. You can format a new dataset using the script.  
```python
cd BIMBA-LLaVA-NeXT
python llava/eval/format_eval_data.py
```
3. Use the following script to evaluate a particular dataset.
```bash
cd BIMBA-LLaVA-NeXT
model_path = "checkpoints/BIMBA-LLaVA-Qwen2-7B"
model_base = "lmms-lab/LLaVA-Video-7B-Qwen2"
model_name = "llava_qwen_lora"
results_dir=results/BIMBA-LLaVA-Qwen2-7B
dataset_name=VideoMME
python llava/eval/infer.py \
    --model_path $model_path \
    --model_base $model_base \
    --model_name $model_name \
    --results_dir ${results_dir}/${dataset_name} \
    --max_frames_num 64 \
    --dataset_name $dataset_name \
    --video_root "path_to_video_folder" \
    --data_path DATAS/eval/VideoMME/formatted_dataset.json \
    --cals_acc
```

### Evaluate All Benchmarks

1. Use the following script to evaluate [PerceptionTest](https://arxiv.org/abs/2305.13786), [NExT-QA](https://arxiv.org/abs/2105.08276), [EgoSchema](https://arxiv.org/abs/2308.09126), [VNBench](https://arxiv.org/abs/2406.09367), [LongVideoBench](https://arxiv.org/abs/2407.15754), [Video-MME](https://arxiv.org/abs/2405.21075), and [MLVU](https://arxiv.org/abs/2406.04264)  benchmarks.
```bash
cd BIMBA-LLaVA-NeXT
bash scripts/video/eval/Eval_BIMBA_LLaVA_Qwen2_7B.sh
```

2. For EgoSchema, use the following script to prepare the submission file.
```python
python llava/eval/submit_ego_schema.py
```
Then, you can either submit directly to the [kaggle competition page](https://www.kaggle.com/competitions/egoschema-public/overview) or use the script for submission and evaluation.
```
kaggle competitions submit -c egoschema-public -f results/BIMBA-LLaVA-Qwen2-7B/EgoSchema/es_submission.csv -m "BIMBA-LLaVA-Qwen2-7B"
```

3. You should get the following results on these benchmarks.

<!-- |               | EgoSchema | VNBench | VideoMME | MLVU | LongVideoBench | NextQA | PerceptionTest |
|:------------:|:--------:|:------:|:--------:|:----:|:--------------:|:------:|:--------------:|
| **Results**  |   71.14   |  77.88  |   64.67   | 71.37 |     59.46      |  83.73  |      68.51      | -->

<table style="border: 1px solid black; border-collapse: collapse;">
  <tr>
    <th style="border: 1px solid black; padding: 8px;">Dataset</th>
    <th style="border: 1px solid black; padding: 8px;">EgoSchema</th>
    <th style="border: 1px solid black; padding: 8px;">VNBench</th>
    <th style="border: 1px solid black; padding: 8px;">VideoMME</th>
    <th style="border: 1px solid black; padding: 8px;">MLVU</th>
    <th style="border: 1px solid black; padding: 8px;">LongVideoBench</th>
    <th style="border: 1px solid black; padding: 8px;">NextQA</th>
    <th style="border: 1px solid black; padding: 8px;">PerceptionTest</th>
  </tr>
  <tr>
    <th style="border: 1px solid black; padding: 8px;">Results</th>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">71.14</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">77.88</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">64.67</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">71.37</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">59.46</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">83.73</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">68.51</td>
  </tr>
</table>




## Citation
If you find BIMBA useful in your research, please use the following BibTeX entry for citation.
```BibTeX
@article{islam2025bimba,
  title={BIMBA: Selective-Scan Compression for Long-Range Video Question Answering},
  author={Islam, Md Mohaiminul and Nagarajan, Tushar and Wang, Huiyu and Bertasius, Gedas and Torresani, Lorenzo},
  journal={arXiv preprint arXiv:2503.09590},
  year={2025}
}
```