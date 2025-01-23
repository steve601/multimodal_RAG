# MultiModal RAG implementation for Video processing
Large language models (LLMs) are text-in, text-out. Large Multi-modal Models (LMMs) generalize this beyond the text modalities. 
For instance, models such as GPT-4V allow you to jointly input both images and text, and output text.
MultiModal RAG is an AI system that understand different modalities like images,audio,video and text.
When building a MultiModal RAG, we must make sure that the modalities we're inputing are images and text only, so we must find a way to convert
audio or video to images and text.

So, how do we build a RAG pipeline in a multi-modal context? There are three different ways we can create an MM-RAG pipeline.

**Option 1**: Use a multi-modal embedding model like CLIP or Imagebind to create embeddings of images and texts. 
              Retrieve both using similarity search and pass the documents to a multi-modal LLM.
**Option 2**: Use MultiModal-LLM like GPT-4 to produce text summaries from images. Embed and retrieve text summaries using 
              a text embedding model. And again, reference raw text chunks or tables from a docstore for answer synthesis by LLM,
              we exclude images from docstore.
**Option 3**: Use a multi-modal LLM to get descriptions of images. Embed the text descriptions using any embedding model of choice and
              store original documents in a doc store. Retrieve summaries with a reference to the original image and text chunks.
              Pass the original documents to a multi-modal LLM for answer generation.

Each of the options has pros and cons.
In this project, we implement option one.

## Getting Started
### Prerequisets
First we install the requirements needed for our project.
### Workflow
1. Download video from Youtube.
2. From the video, extract the images and the audio, then from the audio extract the equivalent text.
3. Create a vector store for both images and text,using LanceDBVectorstore
4. Now create a MultiModal-embeddings for both images and text, using HuggingFaceEmbedding, then create a retriever.
5. Now you can create your prompt template, then load LMM, for my case is Gemini-pro.

### Installation
1. Clone the repo:
   ```bash
   git clone https://github.com/steve601/multimodal_RAG.git
   ```
2. Navigate to the project directory.
3. Follow additional steps if necessary.

## Contributing
Contributions are welcome! Please follow these steps:
1. Fork the project.
2. Create a branch for your feature (`git checkout -b feature-name`).
3. Commit your changes (`git commit -m 'Add new feature'`).
4. Push the branch (`git push origin feature-name`).
5. Open a pull request.