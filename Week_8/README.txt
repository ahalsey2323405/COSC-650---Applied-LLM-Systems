README
This project focuses on creating an AI-powered assistant that can retrieve information from Pololu robotics documentation and use it to answer technical questions based on available evidence.

Techniques Used
This project combines three techniques covered over previous weeks of the course:
• Week 4 – Tool Use: Tools allow the assistant to search documentation or retrieve information from a specific document, providing a structured way to access technical information.
• Week 5 – Retrieval-Augmented Generation (RAG): Documentation is collected from the Pololu website, divided into smaller chunks, converted into embeddings using Sentence Transformers and stored in FAISS indexes. This allows the system to retrieve relevant passages based on a user's question.
• Week 7 – Dynamic Few-Shot Prompting: The system retrieves examples that are semantically similar to the user's question and includes them in the prompt to guide the assistant's response.
These techniques were combined to create a system that retrieves relevant evidence, uses tools to access documentation and generates answers based on the information available.
Evaluation
The system was tested using 10 robotics-related questions. Retrieval performance was measured using the retrieval hit rate at three, while an LLM-as-judge evaluated generated answers on correctness, grounding and relevance using a scale from 1 to 5.
Metric Result
Evaluation cases 10
Retrieval hit rate at 3 90%
Correctness 5/5
Grounding 5/5
Relevance 5/5
The results show that the expected document appeared in the top three retrieved results for 9 out of 10 questions. Correctness, grounding and relevance scores showed the model was consistently calling correct parts of the documentation for the given questions.
One failure occurred when the system was asked to find information about controlling robot motors but failed to retrieve the expected MC33926 motor shield documentation within the top three results. This occurred across all three chunking strategies, suggesting that the broad wording of the question caused the retrieval system to rank other robotics documents more highly. To address this issue, the get_document_info tool was used to search the specific document directly, successfully retrieving relevant passages about motor control. However, this mitigation depends on knowing which document contains the required information.
Technologies Used
• Python and Google Colab
• Sentence Transformers and FAISS
• NumPy
• BeautifulSoup and Requests
• Gemini 3.5 Flash Lite
Running the Project
The notebook requires the relevant Python libraries and an internet connection to retrieve the Pololu documentation. A Gemini API key is also required to generate answers and run the LLM-as-judge evaluation. The notebook should be executed in order from top to bottom, beginning with document collection and retrieval setup, followed by tool configuration, dynamic few-shot prompting and evaluation.
Conclusion
This project demonstrates how multiple AI techniques can be integrated into one system to improve access to technical documentation. Although the evaluation shows promising retrieval performance, the results also demonstrate that retrieving relevant information does not guarantee that every answer will be accurate or complete. Further improvements to retrieval and answer grounding could help make the system more reliable when answering robotics-related questions.