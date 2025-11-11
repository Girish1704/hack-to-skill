# Challenge 3: Add Cross-Domain Intelligence with Azure AI Foundry and Azure AI Search

## Problem Statement

Enterprises often face siloed analytics and fragmented knowledge across departments like HR, Finance, and IT. In this final challenge, you’ll integrate **Azure AI Foundry**, **Azure AI Search**, and **Power Automate** to enable cross-domain reasoning. Your Unified Enterprise Copilot will now perform intelligent query orchestration, provide multi-source summaries, and trigger automated workflows across systems—all through natural language.

## Goals

- Integrate Azure AI Foundry for reasoning and summarization across HR, Finance, and IT data.  
- Use Azure AI Search to perform multi-domain retrieval and correlation.  
- Implement Power Automate workflows for cross-department automation and notifications.  

## Datasets  

- Use the provided datasets in `C:\datasets\` folder:  
  - `hr_policies.xlsx` (HR knowledge base)  
  - `finance_summary.xlsx` (Finance KPIs)  
  - `it_tickets.xlsx` (IT service data)  

These will serve as the knowledge sources for Azure AI Search and cross-domain analysis.

## Challenge Objectives  

1. **Azure AI Foundry Setup**
   - In the Azure portal, create a new **Azure AI Foundry project** named `UnifiedCopilot-Foundry`.
   - Under **Language Models**, deploy:  
     - **GPT-4-turbo** for reasoning and summarization.  
     - **Text-Embedding-3-small** for similarity-based data retrieval.
   - Create a **Custom Prompt Flow** to:  
     - Accept input such as `department` and `query`.  
     - Perform reasoning across indexed data sources.  
     - Return unified insights, e.g.:  
       > “3 unresolved IT tickets are affecting the Finance team’s expense processing system.”

2. **Azure AI Search Integration**
   - Create an **Azure AI Search** resource (Standard S1 tier).  
   - Import data from the three Excel datasets (`hr_policies.xlsx`, `finance_summary.xlsx`, `it_tickets.xlsx`).  
   - Set index name as **enterprise-index**.  
   - Define searchable fields: `Title`, `Description`, `Department`, `Priority`, `DateUpdated`.  
   - Enable **vector search** using the embedding model from Foundry.  
   - Test queries like:
     - `HR attrition rate by cost center`
     - `List IT incidents affecting finance processes`
     - `Show budget allocation for open projects`

3. **Azure Function Orchestration**
   - Create an **Azure Function App** named `cross-domain-func` (HTTP trigger).  
   - Implement logic to:
     - Receive natural-language input from Copilot.  
     - Query **Azure AI Search** for relevant results.  
     - Pass context to **Azure AI Foundry** for reasoning.  
     - Return summarized JSON output such as:
       ```json
       {
         "summary": "Finance processing delays are linked to three unresolved IT incidents.",
         "recommendedActions": [
           "Notify IT team to prioritize ticket closure",
           "Schedule Finance-IT sync meeting"
         ]
       }
       ```
   - Secure with Azure AD authentication and test using Postman or portal console.

4. **Power Automate Integration**
   - Create a **Flow** named `CrossDomainAutomationFlow`.
   - Trigger: When `cross-domain-func` returns a recommendation.  
   - Actions:  
     - **Post message in Teams** → “🚨 IT affecting Finance detected: 3 unresolved tickets.”  
     - **Create approval** → route to IT Manager for escalation.  
     - **Log record in Dataverse** under table `EnterpriseInsights` (fields: Query, Summary, Department, Timestamp).  

5. **Copilot Studio Enhancement**
   - In **Copilot Studio**, add a new topic named **EnterpriseIntelligence**.  
   - Add trigger phrases:
     - `Which IT issues are impacting Finance?`
     - `Show HR attrition trends by cost center.`
     - `Summarize cross-department incidents.`
   - Add an **Action Node** to call the `cross-domain-func` endpoint.  
   - Parse the JSON response and present summaries conversationally.  
   - Example Copilot reply:
     > “There are 3 IT tickets impacting Finance operations. An escalation has been triggered for review.”

6. **Monitoring and Governance**
   - Enable **Application Insights** for the Function App.  
   - Configure **Azure Monitor Dashboard** to track:  
     - Number of cross-domain queries processed.  
     - Function response time.  
     - API call success/failure rates.  
   - Use **Azure API Management** to manage Foundry and Search endpoints with authentication and usage quotas.

7. **Testing**
   - Try the following prompts in Copilot:
     - `List all unresolved IT tickets affecting Finance.`
     - `Show HR leave policy changes impacting payroll.`
     - `Summarize enterprise risks across departments.`
   - Validate if the Copilot provides unified, context-aware responses and triggers automation flows.

## Success Criteria  

- Copilot provides **cross-domain insights** using Azure AI Foundry and AI Search.  
- **Power Automate** successfully triggers workflow actions based on reasoning outputs.  
- All telemetry and audit logs are visible in **Azure Monitor**.  
- Responses are contextually accurate and department-aware.  

## Additional Resources

- [Azure AI Foundry Overview](https://learn.microsoft.com/en-us/azure/ai-studio/)  
- [Azure AI Search Vector Integration](https://learn.microsoft.com/en-us/azure/search/vector-search-overview)  
- [Copilot Studio + Power Automate Integration](https://learn.microsoft.com/en-us/microsoft-copilot-studio/power-automate-integration)  
- [Azure API Management Documentation](https://learn.microsoft.com/en-us/azure/api-management/)  

## Conclusion  

You’ve now built a **cross-domain intelligent Copilot** that bridges HR, Finance, and IT using Azure AI Foundry, Azure AI Search, and Power Automate. This assistant can reason across data silos, summarize enterprise insights, and automate workflows — forming the foundation for a unified, AI-driven enterprise ecosystem.