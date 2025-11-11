# Challenge: Add Talent Insights with Azure AI Foundry & AI Search (Summaries, Sentiment, Trends)
  
## Problem Statement

HR analysts spend hours summarizing engagement responses and spotting trends. In this stage, you’ll connect **Azure AI Foundry** and optional **Azure AI Search** via an **Azure Function façade** to deliver on-demand summaries, sentiment insights, and trend highlights—plus dashboards for HR metrics.

## Goals

- Deploy a GPT-4o-class model (e.g., **gpt-4o-mini**) in **Azure AI Foundry** and **text-embedding-3-small** for vector use cases.
- Build an **Azure Function** that authenticates calls from Copilot and returns summaries/sentiment/trends.
- (Optional) Use **Azure AI Search** to query policy snippets or prior feedback (programmatically seeded).
- Visualize metrics via **Azure Monitor** (Application Insights workbook).

## Datasets / Prerequisites

- **No uploads from `C:\datasets`.**  
- Reuse **Dataverse** rows created in Stage 2 (`PolicyFeedback`) as the analysis corpus.  
- (Optional) Include a tiny, **inline** JSON seed inside the Function for trend demos (e.g., 10 fake survey rows) instead of uploading files.

## Challenge Objectives

1. **Azure AI Foundry**
   - Create a project **HR-Insights-<inject key="Deployment ID" enableCopy="false"/>**.
   - Deploy:
     - **gpt-4o-mini** for summarization/reasoning.
     - **text-embedding-3-small** for embeddings (if you add vector features).
   - Note the **endpoint** and **key**.

2. **Azure Function (Façade)**
   - Create a Function App **func-hr-insights-<inject key="Deployment ID" enableCopy="false"/>** (HTTP trigger).
   - Implement endpoints:
     - `POST /summarize-feedback` → Pull latest `PolicyFeedback` rows from **Dataverse**, group by Topic, call Foundry for **summary + key themes + suggested actions**.
     - `POST /sentiment` → For each row, compute a sentiment label and return counts and examples.
     - `POST /trends` → (Optional) If you want search-like lookups, generate small **in-memory** docs (policy snippets, FAQs) and either:
       - Query directly in-memory, or
       - Upsert them programmatically to a lightweight **Azure AI Search** index named **hr-trends-<inject key="Deployment ID" enableCopy="false"/>** (no file uploads—generate the docs within code).

3. **Copilot Studio Integration**
   - Add **Actions** for:
     - **AnalyzeFeedback** → calls `/summarize-feedback`
     - **GetSentiment** → calls `/sentiment`
     - **ShowTrends** → calls `/trends` (optional if you used AI Search)
   - Create a topic **Talent-Insights** with trigger phrases:
     - `Summarize employee sentiment this quarter`
     - `What are the top 3 HR pain points?`
     - `Any trends in feedback about benefits?`
   - Display structured outputs (e.g., bullets: Themes, % distribution, Recommendations).

4. **Observability with Azure Monitor**
   - Enable **Application Insights** for the Function App.
   - Create a workbook dashboard tracking:
     - Requests by route (summarize/sentiment/trends)
     - Avg latency / failure rate
     - Top themes detected (capture as custom dims)
     - Daily volume and sentiment distribution

5. **Testing**
   - From Copilot, ask:
     - `Summarize employee sentiment for Remote Work policy.`
     - `List top themes and recommendations for leave policy feedback.`
     - `Highlight trends in benefits queries this month.`

6. **(Optional) Proactive Recommendations**
   - Extend the Function to return a `RecommendedActions` list (e.g., “Clarify eligibility wording”, “Publish timeline visual”), and surface as a Copilot reply section.

## Success Criteria

- Copilot returns readable **summaries**, **sentiment breakdowns**, and **trends** based on Dataverse feedback.
- Function façade authenticates and calls Foundry successfully.
- Azure Monitor workbook displays live metrics.

## Additional Resources

- Azure AI Foundry (model deployments)  
- Use Azure OpenAI with your data (RAG quickstart)  
- Application Insights + Workbooks

## Conclusion

You’ve delivered an **intelligent HR Policy & Talent Insights Assistant**: SharePoint-grounded Q&A, Power Automate operational flows, and AI-powered analytics for sentiment and trends—all without uploading local datasets. This completes the HR automation loop from knowledge to action to insights.