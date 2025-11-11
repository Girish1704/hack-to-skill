# Challenge 3: Enable Intelligence and Predictive Insights with Azure AI Foundry and Azure AI Search

## Problem Statement

Finance leaders need real-time insights from documents beyond extraction—understanding trends, anomalies, and financial performance patterns. Manual reviews can’t scale, and disconnected tools hinder proactive analysis.  
In this challenge, you’ll bring **intelligence and reasoning** to the Finance Insight Copilot using **Azure AI Foundry**, **Azure AI Search**, and **Power BI** for visualization.

## Goals

- Connect **Azure AI Foundry** for document summarization, anomaly detection, and reasoning.  
- Index finance document data using **Azure AI Search** for semantic retrieval.  
- Generate AI-driven insights and visualize financial metrics in **Power BI** dashboards.

## Datasets

- Use datasets from `C:\datasets\finance_records.csv` and `C:\datasets\invoice_samples.csv`.  
- These files simulate historical transactions and extracted invoice details.  
- You’ll index them for search and analysis using **Azure AI Search** and Foundry models.

## Challenge Objectives

1. **Azure AI Foundry Setup**
   - In the **Azure Portal**, create a new **Azure AI Foundry project** named `FinanceInsights-Foundry`.
   - Deploy the following models under **Language Models**:
     - **GPT-4-turbo** for reasoning, summarization, and anomaly explanations.
     - **Text-Embedding-3-small** for semantic vector generation.
   - Test model endpoints in Foundry Studio to ensure they return valid summaries for financial text.

2. **Azure AI Search Indexing**
   - Create an **Azure AI Search** resource using **Standard (S1)** tier.
   - Use the **Import Data Wizard** to upload both `finance_records.csv` and `invoice_samples.csv`.
   - Create an index named `finance-insights-index`.
   - Configure fields:
     - `InvoiceID`, `VendorName`, `Amount`, `Tax`, `Total`, `PaymentStatus`, `Date`, and `Comments`.
     - Mark `VendorName` and `Comments` as **searchable** fields.
   - Test the index using the **Search Explorer** to validate search results.

3. **Azure Function Intelligence Connector**
   - Deploy an **Azure Function App** named `finance-ai-analyzer`.
   - Implement logic to:
     - Receive query input (e.g., “Summarize vendor spend this month”).
     - Retrieve relevant documents from Azure AI Search.
     - Send content to **Azure AI Foundry** for summarization and reasoning.
     - Return insights, anomaly flags, and confidence scores.
   - Configure secure authentication between Azure Function, Foundry, and AI Search.
   - Test the endpoint using **Postman** or **cURL**.

4. **Copilot Studio Integration**
   - In **Copilot Studio**, create a new topic named **FinanceInsightsAI**.
   - Add trigger phrases such as:
     - “Summarize vendor spend trends”
     - “Show invoice anomalies this quarter”
     - “What are the biggest unpaid invoices?”
   - Add an **Action Node** that calls the Azure Function endpoint securely.
   - Parse and present summarized insights or anomalies directly in chat.
   - Test with queries like:
     - “Summarize monthly spend per vendor.”
     - “Highlight invoices with inconsistent tax entries.”

5. **Power BI Visualization**
   - Connect **Power BI Desktop** to your **Dataverse** or output CSV dataset.
   - Build dashboards for:
     - Monthly and quarterly spend by vendor.
     - Top anomalies or delayed payments.
     - Aggregated tax and totals visualization.
   - Publish the dashboard to **Power BI Service** and embed its URL in Copilot responses for quick access.

6. **Testing and Validation**
   - Query the Copilot with:
     - “Summarize total quarterly payments and list top 3 vendors.”
     - “Detect any unusual invoice totals this quarter.”
     - “Give me an overview of delayed payments.”
   - Verify:
     - AI Foundry model summaries are contextually relevant.
     - Azure Function returns correct responses.
     - Power BI dashboards update with live financial data.

## Success Criteria

- The Copilot provides summarized financial insights using AI Foundry and AI Search.  
- Azure Function retrieves and processes data accurately with contextual recommendations.  
- Power BI dashboard visualizes anomalies, totals, and spend distributions.  
- Copilot responds to analytical and anomaly-detection queries effectively.

## Additional Resources

- [Azure AI Foundry Overview](https://learn.microsoft.com/en-us/azure/ai-studio/)  
- [Azure AI Search Documentation](https://learn.microsoft.com/en-us/azure/search/search-what-is-azure-search)  
- [Azure Document Intelligence](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/)  
- [Power BI Desktop Overview](https://learn.microsoft.com/en-us/power-bi/fundamentals/desktop-getting-started)

## Conclusion

You’ve successfully built the intelligent layer of the **Finance Document Insight Copilot**.  
Your assistant can now summarize key spend insights, detect anomalies, and deliver data-driven recommendations through a unified conversational interface.  
This stage completes the full automation loop—combining **AI reasoning**, **data retrieval**, and **visual insights** for real-world financial intelligence.