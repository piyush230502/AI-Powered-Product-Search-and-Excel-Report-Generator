# MCP Automation App

## Overview

This application enables users to search and compare products or flight prices across popular e-commerce and travel websites **using natural language queries**.  
It leverages an LLM (Groq, OpenAI, or Ollama) to parse your query and dynamically generates browser automation (using Playwright) for sites like Amazon and Flipkart. Results are compiled into a visually appealing Excel report for easy viewing and analysis.

## Features

- **Natural language search** (e.g., "Find me laptops under ₹50,000")
- **LLM-based query interpretation** (Groq, OpenAI, or local Ollama)
- **Automated browser workflow** (MCP - Micro Command Protocol)
- **Data extraction** from Amazon, Flipkart, etc.
- **Excel report output** with highlights and price comparison chart
- **Logs** for transparency (stored in `logs/`)

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/yourrepo.git
   cd yourrepo
   ```
2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```
3. **Install playwright browsers**
   ```bash
   playwright install
   ```
4. **Set up LLM API keys/environment**
   - For Groq: set `GROQ_API_KEY`
   - For OpenAI: set `OPENAI_API_KEY`
   - For Ollama: ensure Ollama is running with your desired model
   - You can use a `.env` file or export in your shell

## Usage

### Basic Example

Edit and run the sample block in `app.py` or integrate as a Python module.

```python
import asyncio
from app import QueryProcessor

async def main():
    processor = QueryProcessor(llm_provider="ollama", ollama_model="llama3")
    query = "Find me laptops under ₹50,000"
    result = await processor.process_query(query)
    print(result)

if __name__ == "__main__":
    asyncio.run(main())
```

- The generated Excel report will be saved in your working directory.

## Example Queries

- `Find me trimmers under ₹1000`
- `Compare the prices of iPhone 14 on Amazon and Flipkart`
- `Search for flights from Delhi to Mumbai for next Friday`

## Output

- **Excel file** with:  
  - Site, Product Title, Price, Timestamp  
  - Highlights for best deals  
  - Embedded bar chart (price comparison)
- File saved as `query_report_.xlsx`

## How It Works

1. **Parse query:** The LLM returns structured info (`query_type`, sites to search, and product/price data).
2. **Generate MCP steps:** The app creates a workflow (navigate, scroll, type, etc.) for the target sites.
3. **Automate browser:** Playwright performs each step, then data is scraped.
4. **Generate report:** Compile, format, and visualize in Excel.

See [MCP_AUTOMATION.md](MCP_AUTOMATION.md) for technical details of automation command flow.

## Customization & Extensibility

- **Add new sites or workflows:** Update automation and scraping logic per site in `app.py`.
- **Switch LLMs:** Use `llm_provider` parameter and configure API keys or Ollama model.

## Troubleshooting

- **Missing results:** Check your API keys, Ollama model, or ensure products exist on the sites.
- **Ollama:** Run `ollama serve` and ensure selected model is pulled.
- **Logs:** Check `logs/query_processor_*.log` for detailed run info.

## License

MIT License

## Acknowledgments

- [Playwright](https://playwright.dev/python/)
- [Groq](https://groq.com/)
- [OpenAI](https://openai.com/)
- [Ollama](https://ollama.ai/)
- [openpyxl](https://openpyxl.readthedocs.io/)
- [pandas](https://pandas.pydata.org/)

**For more technical detail**, see [MCP_AUTOMATION.md](MCP_AUTOMATION.md).


