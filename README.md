# Text Summarization with T5-Small

## Project Overview

This project implements a complete text summarization system using the T5-small Transformer model. It includes data preprocessing, exploratory data analysis (EDA), model fine-tuning on the CNN/DailyMail dataset, performance evaluation with ROUGE metrics, and deployment through an interactive Gradio interface. The system is capable of generating accurate and concise summaries from long-form news articles in real time.

## Why Use a Summarizer?

Text summarization is important because it helps:

- 🧠 Quickly extract key information from long documents
- ⏱ Save time by condensing large volumes of content
- 📚 Enhance reading comprehension and content curation
- 📈 Improve productivity in academic, legal, medical, and business domains
- 🤖 Enable downstream NLP tasks like indexing, retrieval, and question answering

## Dataset Overview

The model uses the **CNN/DailyMail** dataset — a standard benchmark for abstractive summarization. It contains real-world news articles paired with human-written summaries.

- **Source**: CNN and Daily Mail news websites
- **Task**: Generate concise summaries from long-form articles
- **Language**: English
- **Dataset Size**: ~300,000 article-summary pairs
- **Article Length**: Typically 600–800 words
- **Summary Length**: Typically 50–70 words


* Due to 25MB file upload limit I couldn't upload the dataset.  But you can download it from here:  https://huggingface.co/datasets/abisee/cnn_dailymail/tree/main/3.0.0


## Exploratary Data Analysis 

![image](https://github.com/user-attachments/assets/eff06998-229a-4c1c-b319-d712f9b4a690)

- Average **Article** Length: 790.124
- Average **Summary** Length: 54.8954

    | Metric     | Article Length | Summary Length | Compression Ratio |
    |------------|----------------|----------------|-------------------|
    | **Mean**   | 790.12         | 54.90          | 0.0841            |
    | **Std**    | 382.99         | 21.97          | 0.0481            |
    | **Min**    | 68.00          | 6.00           | 0.0062            |
    | **25%**    | 500.00         | 40.00          | 0.0517            |
    | **50%**    | 717.00         | 52.00          | 0.0731            |
    | **75%**    | 1004.00        | 64.00          | 0.1056            |
    | **Max**    | 2265.00        | 397.00         | 0.7654            |

## Model

- Training a Large NLP Model requires a lot of GPU resources so, I decided to use T5-Small model, It has ~60m parameters which makes it lightweight and very effiecent.


![Capture (1)](https://github.com/user-attachments/assets/3ccce974-a8cb-4875-8350-fa33d9dbee91)

- T5 models are Transformer-based encoder-decoder models.
  
- **Encoder** process input text ---> **Contextual Representation** ---> **Decoder** which generate output tokens one at a time.


## Architecture of T5-Small

  | Component                      | Value  |
  |-------------------------------|--------|
  | Encoder Layers                | 6      |
  | Decoder Layers                | 6      |
  | Attention Heads               | 8      |
  | Hidden Size (d_model)         | 512    |
  | Feed-Forward Layer Dimension  | 2048   |

- It uses 6 encoder and 6 decoder layers, each with 8 attention heads to capture contextual relationships. A hidden size of 512 enables rich embeddings, while a 2048-dimensional feed-forward layer enhances the model’s ability to learn complex language representations.


## Training Configuration

  | Parameter               | Value         |
  |-------------------------|---------------|
  | Pretrained Model        | T5-small      |
  | Epochs                  | 3             |
  | Train Batch Size        | 4             |
  | Eval Batch Size         | 4             |
  | Max Input Length        | 512 tokens    |
  | Max Target Length       | 128 tokens    |
  | Optimizer               | AdamW         |
  | Weight Decay            | 0.01          |
  | Evaluation Strategy     | Per epoch     |
  | Save Best Model         | Based on ROUGE-L |



##  Evaluation 

  | Metric     | Reference Length | Predicted Length | Compression Ratio |
  |------------|------------------|-------------------|-------------------|
  | **Count**  | 200.00           | 200.00            | 200.00            |
  | **Mean**   | 61.16            | 63.19             | 1.193             |
  | **Std**    | 33.75            | 18.97             | 0.514             |
  | **Min**    | 21.00            | 19.00             | 0.157             |
  | **25%**    | 41.00            | 49.00             | 0.794             |
  | **50%**    | 54.00            | 63.00             | 1.114             |
  | **75%**    | 73.25            | 76.25             | 1.521             |
  | **Max**    | 383.00           | 105.00            | 2.524             |

  | Metric     | Precision | Recall | F1 Score |
  |------------|-----------|--------|----------|
  | **ROUGE-1**| 0.3965    | 0.4527 | 0.4027   |
  | **ROUGE-2**| 0.1832    | 0.2068 | 0.1848   |
  | **ROUGE-L**| 0.2654    | 0.3028 | 0.2694   |
  | **ROUGE-Lsum**| 0.3339 | 0.3775 | 0.3376   |

## Results

- Input 

              Title: Global Efforts Intensify as Climate Crisis Drives Extreme Weather Worldwide
      
      Date: June 24, 2025
      
      By: Laura Chen, Global News Network
      
      Geneva, Switzerland – In the wake of record-breaking heatwaves, catastrophic floods, and prolonged droughts across multiple continents, global leaders and climate scientists are issuing urgent calls for accelerated climate action.
      
      The World Meteorological Organization (WMO) released a report on Tuesday confirming that the past 12 months have been the hottest on record, with average global temperatures exceeding the pre-industrial baseline by 1.5°C. This threshold, long considered a red line by the scientific community, signals a heightened risk of irreversible climate tipping points.
      
      “This is not a future scenario. The climate crisis is now,” said WMO Secretary-General Petteri Taalas. “We are seeing the consequences in real-time—rising sea levels, melting glaciers, and the increased intensity of storms and wildfires.”
      
      In South Asia, monsoon rains triggered deadly floods in Bangladesh and northern India, displacing over three million people. Meanwhile, in the Western United States, a combination of heat and drought has led to one of the most destructive wildfire seasons on record, with over 1.2 million acres burned so far.
      
      In response, the United Nations is convening a special climate summit next month in Nairobi, aimed at fast-tracking the implementation of green energy transitions and disaster resilience initiatives. Governments are expected to present updated Nationally Determined Contributions (NDCs) under the Paris Agreement.
      
      While some nations have pledged to increase funding for climate adaptation in vulnerable regions, critics argue that current commitments still fall far short of what is needed. “We’re playing catch-up,” said Dr. Anjali Rao, a climate policy expert at the University of Cape Town. “We need systemic transformation, not incremental fixes.”
      
      Public protests have also intensified. In Berlin, tens of thousands marched last weekend demanding a fossil fuel phase-out by 2030. Similar demonstrations have been reported in major cities from São Paulo to Seoul.
      
      As world leaders prepare for the upcoming summit, the pressure is mounting—not just from activists and scientists, but from the escalating disasters themselves.

- Output

        The past 12 months have been the hottest on record, with average global temperatures exceeding the pre-industrial baseline by 1.5°C. This threshold signals a heightened risk of irreversible climate tipping points, says WMO Secretary-General Petteri Taalas. In South Asia, monsoon rains triggered deadly floods in Bangladesh and northern India, displacing over three million people.

## Deployment

- I used Gradio to deploy the Model.  Unfortunately due to Github file limit **25MB** I couldn't upload the model, but you can train the Model using the Notebook above, then use **Gradio Interface** Notebook to deploy your model.

![image](https://github.com/user-attachments/assets/699ae365-9ee9-4acc-bc2e-21e559fee78e)


## Tools used
Built with HuggingFace Transformers, NLTK, and Gradio.




