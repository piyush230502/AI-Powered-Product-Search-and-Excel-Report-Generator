AI-Powered Query Processor
A Streamlit application for processing natural language queries to search products or flights across e-commerce and travel sites (Amazon, Flipkart, MakeMyTrip) using Groq, OpenAI, or Ollama LLMs. Generates Excel reports with scraped data, charts, and conditional formatting.
Setup Instructions
Prerequisites

Python 3.10+: Install from python.org.
Ollama: Install from ollama.com for local LLM inference.
API Keys:
Groq: Obtain from console.groq.com.
OpenAI: Obtain from platform.openai.com.



Installation

Clone or Create Project Directory:
mkdir query_processor_app
cd query_processor_app


Set Up Virtual Environment:
python3 -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows Command Prompt
.\venv\Scripts\Activate.ps1  # Windows PowerShell


Install Dependencies:
pip install -r requirements.txt
playwright install


Configure API Keys:
export GROQ_API_KEY="your-groq-api-key"    # Linux/Mac
export OPENAI_API_KEY="your-openai-api-key"
set GROQ_API_KEY=your-groq-api-key         # Windows Command Prompt
set OPENAI_API_KEY=your-openai-api-key
$env:GROQ_API_KEY="your-groq-api-key"      # Windows PowerShell
$env:OPENAI_API_KEY="your-openai-api-key"


Configure Ollama:
ollama serve
ollama pull llama3


Project Structure:
query_processor_app/
├── src/
│   ├── query_processor.py
│   ├── app.py
├── docs/
│   ├── README.md
│   ├── MCP_AUTOMATION.md
│   ├── WORKFLOW_EXAMPLES.md
├── logs/
├── sample_outputs/
├── requirements.txt



Usage

Run the Streamlit App:
streamlit run src/app.py

Open http://localhost:8501 in your browser.

Query the Application:

Select an LLM provider (Groq, OpenAI, Ollama).
Enter an Ollama model (e.g., llama3) if using Ollama.
Input a query (e.g., "Find me laptops under ₹50,000", "Flight prices from Delhi to Mumbai on 2025-08-01").
Click "Search and Generate Report".
Download the Excel report if successful.


Check Logs:

Logs are in logs/streamlit_app.log and logs/query_processor_*.log.
Example log (2025-07-19 15:09:00 IST):2025-07-19 15:09:00 - INFO - Query parsed successfully: {"query_type": "product_search", ...}





Troubleshooting

JSONDecodeError with Ollama: Ensure Ollama version is 0.2.0+ and llama3 is pulled. Check logs for invalid JSON.
401 Unauthorized: Verify API keys for Groq/OpenAI.
CancelledError: Ensure proper async cleanup (included in query_processor.py).
Contact: Share log file contents for support.

Last updated: July 19, 2025, 03:09 PM IST
