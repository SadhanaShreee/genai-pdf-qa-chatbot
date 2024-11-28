## Development of a PDF-Based Question-Answering Chatbot Using LangChain

### AIM:
To design and implement a question-answering chatbot capable of processing and extracting information from a provided PDF document using LangChain, and to evaluate its effectiveness by testing its responses to diverse queries derived from the document's content.

### PROBLEM STATEMENT:
The objective is to create a chatbot that can intelligently respond to queries based on information extracted from a PDF document. By using LangChain, the chatbot will be able to process the content of the PDF and use a language model to provide relevant answers to user queries. The effectiveness of the chatbot will be evaluated by testing it with various questions related to the document.

### DESIGN STEPS:

#### STEP 1: Install Required Libraries

#### STEP 2: Create LangChain Components

#### STEP 3: Implement the Chatbot Logic

### PROGRAM:
```
import openai
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain
from langchain.llms import OpenAI
from PyPDF2 import PdfReader

# Step 1: Set OpenAI API Key


# Step 2: Load PDF and Extract Text
def extract_text_from_pdf(pdf_path: str) -> str:
    reader = PdfReader(pdf_path)
    text = ""
    for page in reader.pages:
        text += page.extract_text()
    return text

# Step 3: Define the LangChain components
# Define the prompt template
prompt_template = """
You are a knowledgeable assistant that can answer questions based on the content of a document. 
The document content is as follows:

{document_content}

Please answer the following question:
{question}
"""

# Instantiate the LangChain Prompt Template
prompt = PromptTemplate(template=prompt_template, input_variables=["document_content", "question"])

# Step 4: Define the Model (OpenAI GPT)
def query_pdf_content(pdf_path: str, user_query: str) -> str:
    # Extract text from the PDF
    document_content = extract_text_from_pdf(pdf_path)
    
    # Initialize LangChain with the model and prompt
    model = OpenAI(temperature=0,openai_api_key="your-api-key")
    chain = LLMChain(llm=model, prompt=prompt)

    # Step 5: Run the model with the document content and user query
    response = chain.run({"document_content": document_content, "question": user_query})

    return response

# Example usage
pdf_path = "/content/DSA_INDEX.pdf"  # Replace with your PDF path
user_query = "What is the main topic of the document?"

# Query the chatbot
response = query_pdf_content(pdf_path, user_query)

# Display the result
print(f"Response: {response}")
```

### OUTPUT:
![Screenshot 2024-11-28 215534](https://github.com/user-attachments/assets/ae9a5d33-c366-43f7-b00b-c9e82b9e8ec6)


### RESULT:
The chatbot effectively extracted information from the provided PDF and answered various queries accurately. It demonstrated strong performance in processing and responding to questions based on the document's content.
