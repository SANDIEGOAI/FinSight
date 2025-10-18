# FinSight: An Agentic AI for Investment Research

FinSight is an autonomous AI agent, powered by Google's Gemini, designed to conduct comprehensive financial analysis. It deconstructs user queries, dynamically calls multiple APIs for live data, and synthesizes its findings into a clear report.

What makes FinSight unique is its **Evaluator-Optimizer** loop: after drafting an analysis, it critiques its own work and refines it, learning from each interaction to improve future performance.


## 🚀 Core Features

* **Comprehensive Analysis:** Get a full-stack report on any stock, including:
    * **Financial Health:** P/E, ROE, Debt/Equity, and margin analysis.
    * **Technical Outlook:** RSI, MACD, and EMA trend signals.
    * **Market Sentiment:** Real-time news analysis using FinBERT.
* **Agentic Planning:** The agent intelligently plans which tools to call based on the user's intent (e.g., a full report vs. just technicals).
* **Self-Reflection (Evaluator-Optimizer):**
    1.  The "Analyst" agent writes a draft.
    2.  The "Evaluator" agent critiques the draft for accuracy, depth, and synthesis.
    3.  The "Analyst" refines the draft based on the critique before presenting the final answer.
* **Continuous Learning:** The Evaluator generates a "lesson learned" from each analysis, which is stored in memory and used to improve all future reports.
* **Dynamic Charting:** Automatically generates and displays a comprehensive `.png` chart with candlesticks, EMAs, RSI, and MACD.

## 🏛️ Architecture: The Evaluator-Optimizer Loop

This project uses a multi-agent system to ensure high-quality output.

1.  **User Query:** The user asks, "Tell me about MSFT."
2.  **Analyst Agent (Plan & Execute):** The agent plans its tool calls: `get_company_fundamentals`, `get_technical_analysis`, `get_news_and_sentiment`, and `generate_analysis_chart`. It executes them sequentially.
3.  **Draft Generation:** The Analyst synthesizes all the gathered data into a *draft report*.
4.  **Evaluator Agent (Self-Reflection):** This draft is passed to a *second* AI, the Evaluator. It reviews the draft against strict criteria (e.g., "Did it just list data, or did it connect the dots?").
5.  **Refinement:** The Analyst receives the critique (e.g., "You listed the RSI but didn't explain what it *means*") and rewrites the report to address the feedback.
6.  **Final Output:** The polished, refined analysis is presented to the user.

## 🛠️ Tech Stack & Tools

* **AI Core:** Google Gemini (`gemini-1.5-flash`)
* **Financial Data:** `yfinance` (Yahoo Finance), Financial Modeling Prep (FMP)
* **News & Sentiment:** NewsAPI, `transformers` (Hugging Face `ProsusAI/finbert`)
* **Analysis & Charting:** `pandas`, `pandas_ta`, `mplfinance`

## ⚙️ Setup & Installation

This project is designed to run in **Google Colab**.

1.  **Clone the Repository (or Upload):**
    * Clone this repo and upload the `.ipynb` file to your Google Drive.
    * OR, simply open the `FinSight_Agent.ipynb` file directly in Colab.

2.  **Install Dependencies:**
    The first runnable cell in the notebook installs all required libraries:
    ```python
    !pip install google-generativeai yfinance pandas pandas_ta requests transformers mplfinance
    ```

3.  **Set API Keys:**
    This project requires API keys. Store them securely using Colab's **"Secrets"** manager (click the 🔑 icon on the left).
    * `GOOGLE_API_KEY`: From Google AI Studio.
    * `NEWS_API_KEY`: From [newsapi.org](https://newsapi.org).
    * `FMP_API_KEY`: From [financialmodelingprep.com](https://financialmodelingprep.com).

## ▶️ How to Use

1.  Open the notebook in Google Colab.
2.  Set your API keys in the **Secrets** tab (see above).
3.  Run all cells from top to bottom (Runtime > Run all).
4.  Go to the final cell, **"Cell 6: Run the Agent"**.
5.  Change the query inside the `run_finsight_agent()` function to the stock you want to analyze.

**Example Queries:**
```python
# Run a full report
run_finsight_agent("Give me a comprehensive analysis of Nvidia (NVDA)")

# Get a focused insight
run_finsight_agent("What are the technicals for TSLA?")

# Run a peer comparison
run_finsight_agent("How does Apple (AAPL) compare to its competitors?")
