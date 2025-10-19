🧠 GPT-2 Text Generator App

This project is an interactive Streamlit web application that uses the Hugging Face GPT-2 model to generate text based on a user-provided prompt.
The user enters a starting sentence, selects the maximum output length, and with one click, receives AI-generated text in real time. 🚀

🚀 Features

✅ GPT-2 Model Integration – Powered by Hugging Face’s transformers library.
✅ Streamlit Interface – Simple, interactive web-based UI.
✅ Real-Time Text Generation – Generates coherent text continuations instantly.
✅ Caching Mechanism – Model loads once using @st.cache_resource for efficiency.
✅ Deterministic Output – Reproducible results with set_seed(42).
✅ Adjustable Parameters – Control the maximum number of tokens generated.

🗂 Project Structure
📁 streamlit_gpt2_app/
│
├── streamlit_gpt2_app.py   # Main application file
├── requirements.txt         # (optional) Python dependencies
└── README.md                # Project documentation

🧰 Technologies Used
Technology	Purpose
Python 3.8+	Programming language
Streamlit	For building the web interface
Transformers (Hugging Face)	For GPT-2 model loading and inference
PyTorch / TensorFlow	Backend framework for model computation
Warnings	Used to suppress unwanted warnings during runtime
⚙️ Installation & Setup
1️⃣ Install dependencies

Run the following commands in your terminal:

pip install streamlit transformers torch


(If you prefer TensorFlow instead of PyTorch, you can install tensorflow instead of torch.)

2️⃣ Run the app

To launch the Streamlit app:

streamlit run streamlit_gpt2_app.py


Then open your browser and navigate to:

http://localhost:8501

💡 How It Works

Model Loading

@st.cache_resource
def load_model():
    return pipeline(
        'text-generation',
        model='gpt2',
        tokenizer='gpt2',
        pad_token_id=50256
    )


This function loads the GPT-2 text generation model once and caches it for faster subsequent runs.

User Input

prompt = st.text_area("✍️ Enter your starting sentence:")
max_len = st.slider("📏 Maximum number of words/tokens", 50, 100)


The user provides a prompt and selects the number of tokens to generate.

Text Generation

output = text_generator(
    prompt,
    max_new_tokens=max_len,
    do_sample=True,
    temperature=0.7,
    top_k=50,
    top_p=0.95,
    repetition_penalty=1.2
)


GPT-2 generates text using nucleus sampling and temperature-based randomness for natural, diverse results.

Output Display
The generated text is shown on the web interface:

st.success(output[0]['generated_text'])

🧠 About GPT-2

GPT-2 (Generative Pretrained Transformer 2) is a large-scale language model developed by OpenAI.
It can perform various natural language tasks — from text completion to creative writing and code generation.
This project uses Hugging Face’s transformers library to easily access and run GPT-2 locally or in the cloud.

⚙️ Parameter Explanation
Parameter	Description
max_new_tokens	Maximum number of tokens to generate
temperature	Controls randomness (lower → more predictable, higher → more creative)
top_k	Limits sampling to the top K probable words
top_p	Nucleus sampling threshold for cumulative probability
repetition_penalty	Reduces repeated phrases
pad_token_id	Padding token ID (50256 for GPT-2)
🧪 Example Usage

Input:

Artificial intelligence in the future


Output:

Artificial intelligence in the future could completely transform how humans work and live. New technologies will empower creativity and enhance our ability to solve complex problems.




👩‍💻 Author

Fatima Humbatli
📍 GitHub: fatyaahv  /  fatima.humbatli@gmail.com

💬 Feel free to open an issue for questions or contributions!
