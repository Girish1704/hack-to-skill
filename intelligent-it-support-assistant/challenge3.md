# Challenge 3: Add Intelligence to the IT Support Assistant using Azure AI Foundry and Azure AI Search
  
## Problem Statement

Modern IT assistants must go beyond automation — they should understand, analyze, and recommend. In this challenge, you’ll integrate **Azure AI Foundry**, **Azure AI Search**, and **Azure Monitor** with your Copilot to enable contextual reasoning, intelligent ticket analysis, and support trend insights.

## Goals

- Connect Azure AI Foundry model to analyze IT tickets.
- Build a retrieval-augmented response system for intelligent troubleshooting.
- Visualize telemetry insights using Azure Monitor dashboards.

## Datasets  

- Use the dataset in `C:\datasets\it_tickets_history.csv` to simulate ticket logs and support cases.
- This will be used for AI Search indexing and analysis.

## Challenge Objectives  

1. **Azure AI Foundry Setup**
   - In the Azure portal, create a new **Azure AI Foundry project** named `ITSupport-Foundry`.
   - Under **Language Models**, deploy:
     - **GPT-4-turbo** (for reasoning and summarization).
     - **Text-Embedding-3-small** (for vector creation).

2. **Azure AI Search Setup**
   - Create a **Standard (S1)** tier **Azure AI Search** resource.
   - Use the **Import Data Wizard** to index `C:\datasets\it_tickets_history.csv`.
   - Set index name as **it-support-index**.
   - Validate that documents and fields are properly indexed.

3. **Azure Function Connector**
   - Create a lightweight **Azure Function** (`ticket-analyzer-func`) using HTTP trigger.
   - This function should:
     - Receive user query.
     - Retrieve similar cases from AI Search.
     - Call Foundry model endpoint for summarization.
     - Return recommended resolution.

4. **Copilot Studio Integration**
   - In **Copilot Studio**, add a new topic named **IntelligentAnalysis**.
   - Use the **Action Node** to call your Azure Function endpoint.
   - Configure the Copilot to display the AI model’s summarized insights and recommendations.

5. **Telemetry and Observability**
   - Enable **Azure Monitor** for your Function App.
   - Create a dashboard tracking:
     - Daily tickets resolved.
     - Average response time.
     - Common recurring issues.

6. **Testing**
   - Ask Copilot:
     - `Analyze recent network issues and suggest top 3 causes.`
     - `Summarize high-priority issues from last week.`
     - `Recommend preventive actions for repeated VPN failures.`

## Success Criteria  

- The Copilot provides intelligent recommendations using AI Foundry and AI Search.
- Azure Function returns summarized ticket analysis.
- Azure Monitor dashboard displays metrics successfully.

## Additional Resources:
- [Azure AI Foundry Overview](https://learn.microsoft.com/en-us/azure/ai-studio/)
- [Use your data with Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/use-your-data-quickstart)
- [Azure Monitor Dashboards](https://learn.microsoft.com/en-us/azure/azure-monitor/visualize/workbooks-overview)

## Conclusion  

You have successfully built an intelligent IT Support Copilot capable of reasoning over historical tickets, providing AI-driven insights, and surfacing analytics dashboards for support trends.  
Your assistant now combines conversational AI, automation, and observability completing the Intelligent IT Support lifecycle.
