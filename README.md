## Abstractive Text Summarization using Transformers
This repository is part of the project coursework for CSE-676 at UB for the MS DS program.

With the increased use of e-commerce websites, it is helpful to have a quick and valuable insight of reviews of products bought online, to discern important customer feedback in a short summary, leaving out irrelevant information. While the overall rating provides a general indication of the product’s validity, the customer review section provides a more detailed picture to people who plan on buying the product. We propose an application type project which aims to summarize the customer feedback using Natural Language Processing techniques to improve the buying and selling experience for our target audience: customers and sellers on e-commerce platforms. In this project, we perform Abstractive Text Summarization on product reviews for any given E-commerce platform, for an impactful and improved consumer experience. We are experimenting with 3 models, fine tuning them and comparing their results and analysis.

Following pre-trained models are further finetuned on our dataset :
- facebook/Bart model <br/>
- google/T5 model <br/>
- google/Pegasus model <br/>

## Model weights and Demo
- BART - https://huggingface.co/sumedh/distilbart-cnn-12-6-amazonreviews
- T5 - https://huggingface.co/sumedh/t5-base-amazonreviews
- Pegasus - model weights can be obtained by running the Pegasus_finetuning.ipynb

## Usage 
Install the requirements from req.txt using <br>
`pip install -r req.txt` <br>

To use the model directly in code, use the following snippets, <br>
For T5 model using transformers library <br>
`from transformers import AutoTokenizer, AutoModelForSeq2SeqLM`<br>
`tokenizer = AutoTokenizer.from_pretrained("sumedh/t5-base-amazonreviews")`<br>
`model = AutoModelForSeq2SeqLM.from_pretrained("sumedh/t5-base-amazonreviews")`<br>

For BART model using transformers library<br>
`from transformers import AutoTokenizer, AutoModelForSeq2SeqLM` <br>
`tokenizer = AutoTokenizer.from_pretrained("sumedh/distilbart-cnn-12-6-amazonreviews")` <br>
`model = AutoModelForSeq2SeqLM.from_pretrained("sumedh/distilbart-cnn-12-6-amazonreviews")` <br>

## Dataset
Amazon reviews Dataset was downloaded from [here](https://huggingface.co/datasets/amazon_us_reviews), the finetuned models used english language reviews in the dataset across a subset of product reviews due to the limitation of computational resource constraints.<br/>

## Instructions to run the project:
- You can download the dataset from the current repository: data.csv
- Simply run each notebook and check the results.<br/>
- Run the following notebooks:
  - T5_summarization_for_amazon_us_reviews_cse676.ipynb 
  - BART_finetuning_amazonreviews.ipynb 
  - Pegasus_finetuning.ipynb
- If running these notebooks on colab or any other platform, you need to set output directories or init directories as and where applicable in the notebook

##  Novel techniques used for fine-tuning
During the finetuning process, several techniques for easily fitting the model on low resource systems
were used.
- 8 bit Optimizers: We made use of 8 bit Adam optimizers in the finetuning process which accelerates optimization compared to default 32 bit Adam optimizer but uses    memory that might otherwise be allocated to model parameters, thereby limiting the maximum size of models trained in practice. The 8-bit statistics maintain the performance levels of using 32-bit optimizer states.
- Efficient Batching and learning rate experimentation: We experimented with a combination of smaller batch sizes and higher learning rates for the model to perform optimally based on the resources for training. The chosen combination ensured that the model training remained stable even when the learning rates were higher.
- Gradient accumulation: We implemented gradient accumulation which modifies the last step of the training process. Instead of updating the network weights on every batch, we save gradient values, proceed to the next batch and add up the new gradients. The weight update is then done only after several batches have been processed by the model. Gradient accumulation helps to imitate a larger batch size

## Project report
The project report and more details can be found in the file **sumedhk_hamzaabu_srivast3_kchhajed.pdf**

## References:
- https://shivanandroy.com/fine-tune-t5-transformer-with-pytorch/<br/>
- https://github.com/nlp-with-transformers/notebooks/blob/main/06_summarization.ipynb




