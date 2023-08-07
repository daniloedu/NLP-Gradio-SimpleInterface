# NLP-Gradio-SimpleInterface

## Introduction 
This notebook contains code to build a web-based application for Natural Language Processing (NLP) tasks using the Hugging Face Transformers library.  It includes two main functionalities: text summarization and Named Entity Recognition (NER). The application is built using the Gradio library, which allows us to easily create a user interface for the application.

## Requirements
This application requires the following Python libraries:
1. `os`
2. `io`
3. `IPython.display`
4. `PIL` (Pillow)
5. `base64`
6. `dotenv`
7. `requests`
8. `json`
9. `transformers`
10. `gradio`

In addition to these libraries, you will also need to have a Hugging Face API key, which you can obtain by signing up on the Hugging Face website. This key should be stored in an environment variable named `HF_API_KEY`. The endpoint for the Hugging Face API should be stored in an environment variable named `HF_API_SUMMARY_BASE` for the summarization task and `HF_API_NER_BASE` for the NER task.

## Code Explanation

The code in this notebook is organized into several helper functions and main sections that set up the Gradio interfaces.

### Helper Functions
- `get_completion(inputs, parameters=None, ENDPOINT_URL=os.environ['HF_API_SUMMARY_BASE'])`: This function sends a POST request to the Hugging Face API and returns the response as a Python dictionary. It accepts an `inputs` argument, which is the text to be summarized or the text for NER, and an optional `parameters` argument. The `ENDPOINT_URL` is retrieved from an environment variable.
- `get_completion = pipeline("summarization", model="shleifer/distilbart-cnn-12-6") and get_completion = pipeline("ner", model="dslim/bert-base-NER")`: These lines set up Hugging Face pipelines for the summarization and NER tasks, respectively, using the specified models.
- `summarize(input)` and `ner(input)`: These functions take an `input` (a text string), pass it to the `get_completion` function, and return the generated summary or the recognized named entities.
- `merge_tokens(tokens)`: This function merges consecutive tokens that belong to the same entity in the NER output.

### Gradio Interfaces
The main parts of the notebook set up Gradio interfaces for the text summarization and NER applications. The `gr.Interface` function is used to create the interfaces. The `fn` argument is the function that is called when the user submits a text, `inputs` and `outputs` specify the types of the input and output, and `title` and `description` provide information that is displayed on the interface. The `allow_flagging` argument is set to "never" to disable the flagging feature. Finally, the examples argument provides a list of example texts that the user can try.

The Gradio interfaces are launched with the `launch` method. The `share` argument is set to `True` to generate a public URL for the interface, and the `server_port` argument specifies the port to use for the server.

