# amazon_polarity_aasignment
# Submitted by,
# Name : Bineeth Mathew
# Student_Id :22004878
# 1.0 INTRODUCTION
Thee Amazon Polarity Dataset, which contains over 35 million product reviews classified as positive or negative, provides valuable insights for businesses. Each review includes a rating indicating the customer’s sentiment towards the product. This labeled dataset is highly useful for natural language processing (NLP) and machine learning applications. Companies can leverage the dataset to refine their advertising and marketing strategies by analyzing customer feedback to understand which products are well-received and identifying key features that influence purchasing decisions. Such insights enable targeted marketing campaigns and improved product recommendations. Additionally, the dataset can be employed in recommendation systems to categorize products based on customer sentiment, thereby enhancing the organization and personalization of product recommendations. In this task we will be training a Bert Large language model on amazon polarity reviews dataset. The dataset has each product reviews over the years and each review has been classified as either negative or positive reviews.
# 2.0 Methanology
The BERT Large language model (Bidirectional Encoder Representations from Transformers) to classify reviews into positive or negative categories. BERT was pre-trained on extensive datasets, including Wikipedia and Google's BooksCorpus, which together encompass approximately 3 billion words. This extensive training has endowed BERT with a deep understanding of both the English language and general world knowledge (B. Muller 2022).

BERT utilizes an attention mechanism, a core component of transformer models, to comprehend the relationships between words in a sequence. This mechanism has significantly contributed to the success of transformer-based models in deep learning tasks, particularly in natural language processing (NLP). In this task, we employ BERT for sequence classification, which involves adding a multi-head attention layer to the base BERT model. Each attention head focuses on different patterns within the data. The architecture includes the base BERT model followed by a linear layer specifically designed for classifying sequences into predefined categories—in this case, positive and negative.

The model generates logits, which are raw prediction scores. To determine the final class, activation functions such as sigmoid or softmax are applied, depending on whether the classification is binary or multi-class. The model is compiled using the bert-base-uncased weights, which consist of 110 million parameters. The "uncased" designation means the model processes all text in lowercase, treating words such as "Bag" and "bag" or "America" and "america" as equivalent, thereby ignoring case sensitivity.
# 3.0 EDA
The code visualizes the distribution of word counts and text lengths in reviews based on sentiment. By generating histograms for positive and negative reviews, the functions help analyze the correlation between text characteristics and sentiment, offering insights into how review length and word count differ between sentiments. These visualizations facilitate easy comparison between positive and negative reviews.
# 4.0 Data preprocessing
To prepare the data for training, the BERT tokenizer is initialized using the "bert-base-uncased" model. We first check the dataset for any missing or null values in the 'text' or 'label' fields. The tokenize_function is then defined to tokenize the input text, which includes encoding the text into input IDs and attention masks necessary for a transformer model. Additionally, if a fast tokenizer is used, word IDs are generated to map tokens back to their corresponding words in the original text. This function is applied to the entire training dataset using the map function for efficient processing. Finally, a DataCollatorWithPadding is initialized to dynamically pad the input sequences during training, ensuring they are properly formatted for the model's input requirements.
# 5.0 Training and Fine Tuning

The tokenized dataset was first divided into training and test sets, with 30% allocated to the test set. From the training portion, 20,000 examples from the Amazon dataset were selected after shuffling to create the final training dataset. The model was trained for five epochs, and the total number of training steps was determined based on the size of the training dataset and the number of epochs. A specialized optimizer and learning rate schedule were designed, including a very low initial learning rate of 1e-6, no warmup steps, and a weight decay rate of 0.01 to mitigate overfitting. The model was compiled with sparse categorical cross-entropy as the loss function and accuracy as the performance metric. Throughout training, the model achieved a training accuracy of approximately 93.28% and a validation accuracy of 92.16%, reflecting strong performance on both datasets. The training, conducted on a V100 GPU, was efficient, with each epoch taking around seven minutes, which is effective given the extensive dataset and the complexity of the BERT model.
# 6.0 Deployment
After training, the model was saved to a directory on Google Drive for easy access during deployment. For deployment, the model was integrated with a user interface using the ipywidgets library. This setup allows users to input text through an interactive text box and then click a "predict" button to submit the text. Once submitted, the text is tokenized using the bert-base-uncased tokenizer. The tokenized input is then fed into the trained model for prediction. The model's output is in the form of logits, which are raw prediction scores. To determine the predicted class, we use np.argmax to select the class with the highest probability. Additionally, the model returns the probability that the input text belongs to each class, providing further insight into the classification.
# 7.0 Conclusion
While the model demonstrates impressive predictive performance on the dataset, fine-tuning the pre-trained BERT model for our specific task still demands significant computational resources. For example, completing a single epoch on a V100 GPU takes around 10 minutes. This level of computing power is not typically available on a standard PC, making the process of fine-tuning a BERT model for natural language processing tasks both resource-intensive and time-consuming. Consequently, deploying such models on limited hardware may pose challenges for accessibility and efficiency.
