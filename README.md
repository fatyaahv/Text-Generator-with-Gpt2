# streamlit_gpt2_app.py

import streamlit as st
from transformers import pipeline, set_seed
import warnings

# Uyarıları gizle
warnings.filterwarnings("ignore")
set_seed(42)

# Başlık
st.title("🧠 GPT-2 ile Metin Oluşturucu")
st.write("Hugging Face GPT-2 modeliyle metin üretin. 🎉")

# Modeli yükle (önbelleğe alındığı için tekrar tekrar yüklenmez)
@st.cache_resource
def load_model():
    return pipeline(
        'text-generation',
        model='gpt2',
        tokenizer='gpt2',
        pad_token_id=50256
    )

text_generator = load_model()

# Kullanıcıdan input al
prompt = st.text_area("✍️ Başlangıç cümlesini girin:")
max_len = st.slider("📏 Maksimum kelime/token sayısı", 50, 100)

# Buton
if st.button("🚀 Metni Oluştur"):
    with st.spinner("Metin üretiliyor..."):
        output = text_generator(
            prompt,
            max_new_tokens=max_len, 
            num_return_sequences=1,
            do_sample=True,
            temperature=0.7,
            top_k=50,
            top_p=0.95,
            repetition_penalty=1.2,
            pad_token_id=50256,
            truncation=True
        )
        st.subheader("📝 Oluşturulan Metin:")
        st.success(output[0]['generated_text'])
