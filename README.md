## Fine-tuning-SLM

Supervised fine-tuning and Direct preference optimization

Dataset: (https://huggingface.co/datasets/truthfulqa/truthful_qa)<br>
model: https://huggingface.co/Qwen/Qwen2.5-3B<br>
Training stage: Pre-training<br>
Dataset length = 817 fields

### Stage 1: Supervised Fine-tuning

Trained for 27 epochs<br>
#### Insights

| Metric        | Trend         | Comment                      |
|---------------|---------------|------------------------------|
| Train Loss    | ↓↓ steady     | Learning is happening        |
| Val Loss      | ↓→ plateau    | Small improvements still     |
| BLEU          | ↑ slow        | Expected for long answers    |
| ROUGE         | ↑ steady      | Good improvement             |
| BERTScore F1  | ↑ slow & high | Semantic similarity is strong |


#### Metrics Summary

| Metric        | Start Value | Best Value | Best Epoch | % Improvement |
|---------------|-------------|------------|------------|----------------|
| BLEU          | 0.1186      | 0.2149     | 25         | +81.1%         |
| ROUGE-1       | 0.5019      | 0.5949     | 23         | +18.5%         |
| ROUGE-L       | 0.4541      | 0.5658     | 24         | +24.6%         |
| BERTScore F1  | 0.8646      | 0.8781     | 24         | +1.57%         |

#### Train loss
![train-loss](https://github.com/user-attachments/assets/9c76aa15-453c-40c0-9835-4cafece6bc0c)


#### Eval loss

![eval-loss](https://github.com/user-attachments/assets/ff5ad2c1-c7ab-4545-b831-aac26431b0f2)

### Stage 2: Direct Preference Optimization

Trained for 5 epochs<br>
#### Insights


| **Metric**           | **Trend**       | **Comment**                                               |
|----------------------|------------------|------------------------------------------------------------|
| Reward (Chosen)      | ↑ moderate       | Model outputs are aligning better with reward model        |
| Reward (Rejected)    | ↓ to < 0         | Rejected completions scored worse (clearer separation)     |
| Reward Accuracy      | ↑ strong         | Preference agreement with reward model is improving        |
| Reward Margin        | ↑ consistent     | Chosen vs. rejected gap is increasing                      |




#### Metrics Summary

| **Metric**           | **Start Value** | **Best Value** | **Best Epoch** | **% Change**        |
|----------------------|------------------|----------------|----------------|----------------------|
| Reward (Chosen)      | 0.1985           | 0.2704         | 3              | +36.2%               |
| Reward (Rejected)    | 0.0755           | -0.0235        | 5              | -131.1%              |
| Reward Accuracy      | 0.7546           | 0.8588         | 4–5            | +13.8%               |
| Reward Margin        | 0.1230           | 0.2900         | 5              | +135.8%              |

