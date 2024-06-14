# School-Info-Chatbot-Hyderabad
A chatbot designed to assist students and parents in Hyderabad schools by providing quick access to information and facilitating communication.

## How to Run the Project

### Prerequisites

Ensure you have the following installed:
- Python 3.7 or higher
- pip (Python package installer)
- Git
- A token for accessing the llama-2 model (if required)

### Steps to Run

#### Clone the Repository

First, clone the repository to your local machine using Git:

```bash
git clone https://github.com/your-username/HyderabadSchoolChatbot.git
cd HyderabadSchoolChatbot
```

#### Install Required Packages

Install the necessary Python packages using `pip`:

```bash
pip install --no-deps "xformers<0.0.26" trl peft accelerate bitsandbytes
pip install milvus pymilvus
pip install gradio
pip install beautifulsoup4
```

#### Data Collection and Preprocessing

Before running the chatbot, you need to collect and preprocess the data. Follow these steps:

1. **Data Collection**

   Ensure you have the JSON data files that were scraped from `yellowslate.com`. These files should be placed in the `files_for_chatbot` directory within the project.

2. **Run Data Collection Script**

   Run the provided data collection script to scrape and collect data:

   ```bash
   python data_collection.py
   ```

3. **Run Preprocessing Script**

   Preprocess the collected data to prepare it for embedding:

   ```bash
   python data_preprocessing.py
   ```

These scripts will generate the necessary JSON files and preprocess them for the chatbot.

#### Run the Notebook

Open and run the Jupyter notebook in Google Colab or locally to set up the chatbot. Follow these steps:

- Open Google Colab.
- Upload the notebook (`chatbot_notebook.ipynb`).
- Execute each cell in the notebook sequentially to set up and run the chatbot.

#### Run the Chatbot Interface

To test the chatbot interface manually before deploying it with Gradio:

```python
query = input("Enter your query:")
print(chatbot.search(query))
```

#### Set Up Gradio Interface

The Gradio interface provides a user-friendly way to interact with the chatbot:

```python
import gradio as gr

with gr.Blocks() as demo:
    with gr.Row():
        with gr.Column(scale=2):
            gr.Markdown('''## Chat''')
            conversation = gr.Chatbot(label='conversation')
            question = gr.Textbox(label='question', value=None)
            send_btn = gr.Button('Send Message')
            send_btn.click(
                fn=respond,
                inputs=[question],
                outputs=conversation,
            )
            question.submit(fn=respond, inputs=[question], outputs=[conversation, question], queue=False)
    
demo.launch(debug=True)
```

#### Close the Interface

Once done, you can close the Gradio interface and stop the Milvus server to free up resources:

```python
demo.close()
default_server.stop()
```

### Notes

- Ensure the Milvus server is running before executing the cells that interact with it.
- The chatbot is designed to work on GPU if available; otherwise, it defaults to CPU.
- You will need a token to access the llama-2 model, if applicable.
- Modify paths and parameters as necessary to fit your local setup and requirements.

This detailed guide should help you set up and run the project effectively. If you encounter any issues, please refer to the project documentation or open an issue in the repository.

### Preview image after running Gradio Interface
![image](https://github.com/Suhail372/School-Info-Chatbot-Hyderabad/assets/116452539/47f766d1-4e7e-4a87-977f-2851f192f5d6)

