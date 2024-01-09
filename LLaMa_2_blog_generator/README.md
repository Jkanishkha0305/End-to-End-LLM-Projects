
# Blog Generator

This is an end to end LLM project based on Meta's LLaMa 2 and Langchain. A system that can generate blogs based on the topic and word limit provide by the user.

## Project Highlights

- Generate Blogs from user provided topic and the word limit 
- We will build an LLM based question and answer system that will use following,
  - Meta LLaMa
  - Streamlit for UI
  - Langchain framework

- In the UI, user will ask questions in a natural language and it will produce the answers


## Installation

1.Clone this repository to your local machine using:

```bash
  git clone https://github.com/Jkanishkha0305/End-to-End-LLM-Projects.git
```
2.Navigate to the project directory:

```bash
  cd LLaMa_2_blog_generator
```
3. Install the required dependencies using pip:

```bash
  pip install -r requirements.txt
```

## Usage

1. Run the Streamlit app by executing:
```bash
streamlit run main.py

```

2.The web app will open in your browser where you can ask questions

## Sample Prompts
  - Write a blog on messi winning the world cup in 350 words
  - Write a blog on forest fires in australia in 1000 words

## Project Structure

- main.py: The main Streamlit application script.
- langchain_helper.py: This has all the langchain code
- requirements.txt: A list of required Python packages for the project.

