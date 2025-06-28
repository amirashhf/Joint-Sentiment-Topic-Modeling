# 🤖 Joint Sentiment-Topic Modeling for Amazon Reviews

![Deep Learning](https://img.shields.io/badge/Deep_Learning-PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![NLP](https://img.shields.io/badge/NLP-Transformers-blue)
![BERT](https://img.shields.io/badge/BERT-Model-green)
![Sentiment Analysis](https://img.shields.io/badge/Sentiment-Analysis-yellow)

## 📖 Overview
In e-commerce, user reviews contain a wealth of information. However, analyzing sentiment (is the review positive or negative?) and topic (what is the review about?) are often performed as separate, inefficient tasks. This project addresses this gap by developing and implementing a novel **joint sentiment-topic model**. The model simultaneously performs sentiment classification and topic clustering on Amazon product reviews, providing a more efficient and context-aware analysis that understands *what* users are talking about and *how* they feel about it in a single pass.

## 📊 Dataset
* **Source:** The [Amazon Product Reviews](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt) dataset, specifically from the "Musical Instruments" category.
* **Content:** A subset of **14,000 user reviews** was used for this project due to GPU limitations.
* **Filtering:** The data was filtered to include only reviews with **1, 2 (negative), and 5 (positive)** star ratings to create a dataset with clear sentiment polarity.
* **Columns Used:** `overall` (the star rating) and `reviewText` (the user's comment).

## ⚙️ Model Architecture & Workflow
The core of this project is a unified deep learning model that integrates an autoencoder with a sentiment classifier, built upon modern transformer embeddings.

1.  **Text Pre-processing:** Standard text cleaning procedures were applied to the raw review text.
2.  **BERT Embeddings:** The pre-trained **XLM-Roberta** model was used to convert text into rich, contextual vector representations that capture deep semantic meaning.
3.  **Joint Model Core:**
    * An **Encoder** processes the BERT embeddings into a latent feature space.
    * This latent representation is then fed into two parallel heads:
        * A **Clustering Head** using Deep Embedded Clustering (DEC) to group reviews into thematic topics.
        * A **Sentiment Classification Head** to predict the sentiment (positive/negative).
4.  **Unified Training:** The model is trained end-to-end by optimizing a **combined loss function** derived from both the clustering and sentiment classification tasks, allowing each task to inform and improve the other.

![image](https://github.com/user-attachments/assets/74343bfb-cae3-40e7-90e6-909dd47c8747)

![image](https://github.com/user-attachments/assets/cb740eac-79ea-4a59-8dad-02ceb2d754de)


## 📈 Results & Performance

#### Model Performance
After several experiments, the best-performing model achieved a sentiment classification **accuracy of 91.43%**.

#### Topic Modeling & Sentiment Distribution
The clustering component successfully identified **4 distinct topics**. By analyzing the sentiment distribution within each topic, we can gain valuable business insights:

* **Topic 0: Product Quality & Price:** Sentiment was balanced but leaned slightly negative (13.4% neg vs. 12.3% pos), indicating users are highly sensitive to the value proposition.
* **Topic 1: Accessories & Usage Suitability:** This was the most discussed topic and had the highest positive sentiment (19.2% pos vs. 9.7% neg), suggesting that included accessories are a major driver of customer satisfaction.
* **Topic 2: Product Specifications & Physical Fit:** This topic was predominantly positive, indicating that product descriptions and specifications generally meet customer expectations.
* **Topic 3: Musical Devices & Initial Setup:** This topic was dominated by negative sentiment (11.1% neg vs. 3.3% pos), highlighting common user frustrations during the initial setup and first use of the musical devices.

![image](https://github.com/user-attachments/assets/e972050d-fcc8-40f9-9de5-e510f2a68cb9)
