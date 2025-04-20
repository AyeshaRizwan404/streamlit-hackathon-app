# streamlit-hackathon-app
import streamlit as st
import pandas as pd
import plotly.express as px

# Title of the app
st.title("AI Data Explorer")

# Step 1: File Upload
file = st.file_uploader("Upload your CSV file", type=["csv", "xlsx"])
if file:
    if file.name.endswith('.csv'):
        df = pd.read_csv(file)
    else:
        df = pd.read_excel(file)
    
    # Display data preview
    st.write("Data Preview:")
    st.dataframe(df.head())

    # Step 2: Data Cleaning
    st.write("Missing Values Summary:")
    st.write(df.isnull().sum())

    st.write("Data Types:")
    st.write(df.dtypes)

    # Option to clean missing values
    if st.button("Clean Missing Values"):
        df_cleaned = df.fillna(df.mean())  # Simple way to fill missing values with column mean
        st.write("Cleaned Data:")
        st.dataframe(df_cleaned.head())

    # Step 3: Visualization
    st.write("Visualizations:")
    col = st.selectbox("Pick a column to visualize:", df.columns)
    chart = px.histogram(df, x=col)
    st.plotly_chart(chart)

    # Step 4: Ask a Question (Basic Example)
    question = st.text_input("Ask a question about the data:")
    if question:
        st.write("⚠️ AI Question Answering Coming Soon...")

    # Step 5: Export Option
    if st.button("Export Report"):
        st.write("📄 Report Export Coming Soon...")

