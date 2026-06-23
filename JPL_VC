import pandas as pd
from itertools import zip_longest
import streamlit as st

tenses = ["自动", "他动", "接尾词", "副词", "助词"]

# 1. Choose input mode
mode = st.selectbox("Input mode", ["Plain Text", ".txt File"])
file_lines = []

# 2. Extract lines based on mode
if mode == "Plain Text":
    text_data = st.text_area("Paste your text here (one entry per line):")
    if text_data:
        # Split text into a list of lines, removing empty lines
        file_lines = [line.strip() for line in text_data.splitlines() if line.strip()]
else:
    uploaded_file = st.file_uploader("Upload your file", type=["txt"])
    if uploaded_file is not None:
        # Decode bytes from uploaded file into strings
        file_lines = [line.decode("utf-8").strip() for line in uploaded_file if line.strip()]

# 3. Only run processing logic if we actually have data
if file_lines:
    options = ["Full List"] + tenses
    selected_option = st.selectbox("Select a category to filter or view all:", options)

    v_dict = {}

    if selected_option != "Full List":
        v_dict[selected_option] = [line for line in file_lines if selected_option in line]
    else:
        for tense in tenses:
            v_dict[tense] = [line for line in file_lines if tense in line]

    a = list(zip_longest(*v_dict.values(), fillvalue=""))
    df = pd.DataFrame(a, columns=v_dict.keys())
    st.dataframe(df)
else:
    st.info("Please provide text input or upload a file to begin.")
