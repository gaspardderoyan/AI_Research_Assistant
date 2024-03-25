# Literature Review table using LLM on papers

I have a project to create an app that would be an assitant in doing a literature review or dissertation/thesis. Given some PDF files, the app would first add them to a table, then extract separately the text and the images. The text would be processed into embeddings, and the images with an LLM with vision, adding the context in the query. Then, it would use an LLM (with the option to choose between local ones in Ollama, or others like GPT-4 or Gemini) to fill the columns, using different prompts for different type of information. Some metadata would also be filled using the DOI/ISBN. This should all be saved in a database. It should also be possible to ask questions to the whole database (both the embeddings of the PDF, as well as the full output table). It would have a front-end using Streamliy, which would be deployed using ngrok.

# Project's sub sections

## **Introduction**

- Project overview
- Objectives
- Limitations

## **Literature Review methods**

- Gap Analysis

## **Methodology & System Architecture**

## **Preparation**

- Set the thesis topic & context

## **Data collection and processing**

- PDF
  - Text (PyMuPDF)
  - Image (OpenCV)
- Metadata lookup (DOI/ISBN, crossref api)

## **Embeddings & vector db**

## **LLMS**

- Selection of models (ollama, gpt-4, gemini)
- Filling the table
- Chatbox

## **Database**

- Database Selection (e.g., DuckDB)
- Schema Design
- Data Insertion and Retrieval Mechanisms

## **UI**

- framework (streamlit)
- components
  - set thesis topic
  - customise columns
  - upload pdf's
  - interactive table
  - chatbox (with default and custom queries)

## **Output and Export Options**

- Export Formats (CSV, Markdown, Notion, Audio)
- Customization of Output

## **Advanced Features**

- Querying the Database from the chat
- Comparative Analysis and Summarization
- Integration with Graph Databases (e.g., Neo4j)

## **Deployment (ngrok)**

# Problematics

- Options to give context of the dissertation's topic.
- How to process text AND images/graphs?
  - Maybe manually?
  - PyMuPDF
- How to make sure the output isn't repetitive?
  - Feed in previous inputs as context?
  - Implement a feedback loop that uses similarity detection in the generated outputs to avoid repetitive content. This can be achieved by comparing new outputs with existing entries in the database and adjusting the prompts accordingly
- Should I use embedding on the output text from Vision, or should I feed it whole in the input?
- How to detect the typical papers subparts (abstract, etc)?
- Could I do something to extract all the references mentionned? As well as the context of how and why it was used? And maybe counting the number of times each one is used?
  - Use regular expressions and heuristic methods to identify common sections of academic papers, such as abstracts, methodology, etc. For reference extraction, consider NLP techniques specialized in recognizing citations and references within text.
- Where to export the output? As csv? Notion? Markdown? Audio?
- Add general instructions to explain my research briefly, as well as specific instructions for each columns
- Use a "review" agent to improve upon a fully filled row ... Or on the whole table once it's complete
- Keep all in a database, then have the ability to query on the go: Question + context + RAG
- type of queries for chatbot
  - write quoting a study
  - compare studies (use table output, not embeddings, because RAG bad for lot)
  - generate Pre-made sentences quoting the paper in my diss
  - ask in which papers a reference was quoted, and in which context
- not only pdf, also be able to provide links
- when papers are short enough, create embeddings but don't use them when generating the table's answer / when querying only this paper.
- storing the chat history in a database
- should vectors be altogether, or split by paper? and text/vision, split or together?

# Table Structure

- Title
- Authors
- Journal, Publisher, etc
- Date
- Citation count
- DOI/ISBN
- URL
- Abstract
- Summary
- Literature Review
- Experiments
- Methods
- Statistics
- Conclusion
- Limitations
- Future Research
- How does this paper relate to my research? Why is it important?
- Specific questions (options to custom)
  - Which flow scales were used?

# Implementation & Packages

- **Embeddings**: OpenAi, Ollama
- **Vector**: Chroma, AI_Search (MS Azure)
- **Models**: Ollama, GPT 4, Azure
- **Front**: Streamlit
- **Deploy**: ngrok
- **Audio export**:
- Langchain

# Random Ideas

- Citation Management: Connect to reference management tools (Zotero, Mendeley) for easy import/export.
- Knowledge Graph: Visualize connections between papers, authors, and topics.
  - graphRag? (log4j, neo4j)
- promptFlow
