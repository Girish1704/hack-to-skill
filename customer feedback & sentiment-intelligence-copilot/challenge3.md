# Challenge 3: Add Intelligence to the Customer Feedback & Sentiment Intelligence Copilot using Azure AI Foundry and Azure AI Search
  
## Problem Statement

Customer experience teams must go beyond data collection — they need intelligence. In this challenge, you’ll connect Azure AI Foundry, Azure AI Language, and Azure AI Search to create a unified intelligence layer for feedback summarization, sentiment trends, and proactive alerts. The goal is to empower your Copilot to deliver actionable insights from multi-channel feedback automatically.

## Goals

- Use Azure AI Foundry to analyze cross-channel feedback for sentiment and topic clustering.
- Implement a retrieval-augmented insight system using Azure AI Search for intelligent querying.
- Visualize sentiment and trend insights through Azure Monitor or Power BI dashboards.

## Datasets  

- Use the dataset in `C:\datasets\customer_feedback_history.csv` to simulate customer feedback records from multiple channels.
- This dataset includes feedback text, channel source, sentiment labels, and timestamps — ideal for trend analysis and model evaluation.

## Challenge Objectives  

1. **Azure AI Foundry Setup**
   - In the Azure portal, create a new **Azure AI Foundry project** named `CustomerSentiment-Foundry`.
   - Under **Language Models**, deploy:
     - **GPT-4-turbo** (for summarization and reasoning).
     - **Text-Embedding-3-small** (for similarity search and clustering).
   - Create a **Custom Prompt Flow** that:
     - Takes feedback text as input.
     - Returns sentiment summary, topic clusters, and top recommendations.
     - Outputs a structured JSON response.

2. **Azure AI Search Setup**
   - Create a **Standard (S1)** tier **Azure AI Search** resource.
   - Use the **Import Data Wizard** to index the file `C:\datasets\customer_feedback_history.csv`.
   - Set the index name as **customer-feedback-index**.
   - Ensure fields like `FeedbackText`, `Channel`, and `SentimentScore` are searchable and filterable.
   - Validate that all entries are indexed properly.

3. **Azure Function Integration**
   - Create an **Azure Function** named `feedback-intelligence-func` using an HTTP trigger.
   - Implement logic to:
     - Accept feedback queries from Copilot.
     - Query Azure AI Search for matching records.
     - Call the **Azure AI Foundry endpoint** for analysis and summarization.
     - Return structured responses such as:
       ```json
       {
         "TopThemes": ["Delivery delays", "Support response time"],
         "OverallSentiment": "Mostly positive (78%)",
         "RecommendedActions": ["Improve SLA reminders", "Add proactive follow-ups"]
       }
       ```
   - Enable Application Insights for observability and performance tracking.

4. **Copilot Studio Integration**
   - In **Copilot Studio**, add a new topic called **FeedbackInsights**.
   - Add trigger phrases like:
     - `Summarize this month's customer sentiment.`
     - `What topics are trending in support feedback?`
     - `Highlight negative themes from email feedback.`
   - Create an **Action Node** that calls your Azure Function endpoint.
   - Pass parameters such as date range, sentiment filter, and channel.
   - Parse and present the structured response in a readable conversational format.

5. **Sentiment Alerts & Dashboards**
   - Extend **Power Automate** to:
     - Monitor negative sentiment spikes via Azure Function outputs.
     - Trigger Teams notifications to CX leads when thresholds exceed defined limits.
   - Connect **Azure Monitor** or **Power BI** to visualize:
     - Sentiment trends by channel (Email, Chat, Social).
     - Top topics influencing NPS or CSAT.
     - Volume and trend graphs with average sentiment score.
   - Optionally, add alert rules for anomalies (e.g., “>20% negative feedback in 24 hrs”).

6. **Testing**
   - Test with queries such as:
     - `Summarize top negative topics this month.`
     - `What’s trending in customer chat feedback?`
     - `Show me sentiment changes over the last 7 days.`

## Success Criteria  

- The Copilot returns summarized sentiment insights using Azure AI Foundry and Azure AI Search.
- Azure Function successfully orchestrates data retrieval and model execution.
- Alerts are triggered automatically when sentiment thresholds are breached.
- Dashboards display dynamic sentiment and topic trends.

## Additional Resources

- [Azure AI Foundry Overview](https://learn.microsoft.com/en-us/azure/ai-studio/)
- [Azure AI Language Documentation](https://learn.microsoft.com/en-us/azure/ai-services/language-service/overview)
- [Use your data with Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/use-your-data-quickstart)
- [Azure Monitor Dashboards](https://learn.microsoft.com/en-us/azure/azure-monitor/visualize/workbooks-overview)

## Conclusion  

You’ve built an intelligent **Customer Feedback & Sentiment Intelligence Copilot** that transforms raw feedback into actionable insights. By combining conversational AI, sentiment analysis, and automated alerting, your Copilot empowers CX teams to act faster, improve service quality, and continuously enhance customer satisfaction.