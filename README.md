import requests
import streamlit as st
st.set_page_config(page_title="POS MALAYSIA", page_icon= "🚚", layout="wide")

def load_lottieurl(url):
    r = requests.get(url)
    if r.status_code != 200:
        return None
    return r.json()

# Use local CSS
def local_css(file_name):
    with open(file_name) as f:
        st.markdown(f"<style>{f.read()}</style", unsafe_allow_html= True)

local_css("style/style.css")              

# Header section
with st.container():
    st.subheader("Hello, welcome to POS Malaysia!")
    st.title("POS MALAYSIA BERHAD")
    st.write("Your trusted Malaysian courier &amp; logistics provider | Pos Laju")
    st.write("[Learn more](https://pythonandvba.com)")
   
# Sample dataset
dataset = [
    "Pos Malaysia",
    "Pos Aviation",
    "Pos Logistics",
    "FInance",
    "Retails",
]

st.write("---")
# Dictionary mapping options to PDF URLs
pdf_mapping = {
    "CORPORATE MATTERS": "file:///C:/Users/user/Desktop/kakak/Pos%20Malaysia/AP/MDA.pdf",
    "CONTRACTS & PURCHASES": "url_to_pdf_2",
    "LEGAL MATTERS": "url_to_pdf_3",
    "FINANCE, ACCOUNTING AND TREASURY" : "url_to_pdf_4"
}

# Create a select box
selected_option = st.selectbox("Select an option", list(pdf_mapping.keys()))

# Get the selected PDF URL
selected_pdf_url = pdf_mapping.get(selected_option, "")

# Display the selected PDF hyperlink using st.markdown
pdf_hyperlink = f'<a href="{selected_pdf_url}" target="_blank">Open PDF in New Tab</a>'
st.markdown(pdf_hyperlink, unsafe_allow_html=True)

# Streamlit app
def search_engine(query, data):
    results = [item for item in data if query.lower() in item.lower()]
    return results

# Streamlit UI
st.subheader("Search Engine")

# Search input box
query = st.text_input("Enter your search query:")

# Search button
if st.button("Search"):
    # Perform search and display results
    results = search_engine(query, dataset)

    # Display results
    if results:
        st.header("Search Results:")
        for result in results:
            st.write(result)
    else:
        st.info("No results found.")

# About myself
with st.container():
    st.write("---")
    left_column, right_column = st.columns(2)
    with left_column:
        st.header("About POS MALAYSIA")
        st.write("##")
        st.write("[Youtube Channel](https://youtube.com/c/CodingIsFun)")

# Contact
with st.container():
    st.write("---")
    st.header("Get In Touch With Us!")
    st.write("##")

# Documentation form submit
contact_form = """
<form action="https://formsubmit.co/nurdanishaelfina@gmail.com" method="POST">
     <input type="hidden" name="_captcha" values="false">
     <input type="text" name="name" placeholder ="Your name" required>
     <input type="email" name="email" placeholder = "Your email" required>
     <textarea name = "message" placeholder = "Your message here" required></textarea>
     <button type="submit">Send</button>
</form>
"""
left_column, right_column = st.columns(2)
with left_column:
    st.markdown(contact_form, unsafe_allow_html= True)
with right_column:
    st.empty()    

# Disable the Streamlit watermark
st.set_option('deprecation.showPyplotGlobalUse', False)
