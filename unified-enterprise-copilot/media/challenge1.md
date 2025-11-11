# Challenge 1: Build a Cross-Domain FAQ Copilot with Copilot Studio (Foundation)

## Problem Statement

Employees often need answers that span multiple departments (HR, Finance, IT) but information is scattered across different portals and files. In this foundation stage, you’ll build a **prototype Copilot** in Copilot Studio that can answer **simple cross-domain FAQs** grounded in curated content (SharePoint/Excel). This creates a single conversational entry point before you wire up live systems in later stages.

## Goals

- Create a Copilot Studio agent that answers **HR/Finance/IT FAQs** from a curated knowledge base.  
- Ground responses using **SharePoint or Excel** sources (static content).  
- Publish the agent to **Teams** (or Demo Web App) for quick access.

## Datasets

- Use sample FAQ files from your lab VM (prepare or adapt as needed):  
  - `C:\datasets\hr_faq.xlsx`  
  - `C:\datasets\finance_faq.xlsx`  
  - `C:\datasets\it_faq.xlsx`

> If these files don’t exist, create simple two-column sheets (`Question`, `Answer`) and save them to the paths above.

## Challenge Objectives

1. **Prepare the Knowledge Base (SharePoint or Excel)**
   - Create a SharePoint site (e.g., **enterprise-kb**) and a **Documents** library folder **/FAQs**.
   - Upload the three Excel files from `C:\datasets\` to **/FAQs**.
   - Validate each workbook has a table or header row with **Question** and **Answer** columns.

2. **Create the Copilot Agent**
   - Open **Microsoft Copilot Studio** → **+ New agent**.  
   - Name: **UnifiedCopilot-Foundation** (Category: Enterprise).  
   - Create the agent with default language/region.

3. **Add Knowledge via Generative Answers**
   - In your agent, add a **Generative Answers** capability (Knowledge sources).  
   - Select **SharePoint** as the source and point it to the **/FAQs** folder you created.  
   - (Alternative) If SharePoint isn’t available, upload each FAQ Excel file as a **file source** in Knowledge.

4. **Create Cross-Domain Topics (Optional Enhancers)**
   - Add three topics to guide conversations and surface suggested prompts:
     - **HR-FAQ** — trigger phrases: `HR help`, `leave policy`, `benefits`
     - **Finance-FAQ** — trigger phrases: `expense policy`, `invoice`, `reimbursement`
     - **IT-FAQ** — trigger phrases: `VPN`, `password reset`, `raise IT ticket`
   - In each topic, add a **Generative Answers** node to pull from the knowledge base.

5. **Grounding & Safety Settings**
   - In the **Generative Answers** node, enable **Respond only with data from the selected sources** (to avoid hallucinations).  
   - Add a fallback message when content isn’t found:  
     > “I couldn’t find this in our current FAQs. Try rephrasing or pick a department: HR, Finance, or IT.”

6. **Publish the Agent**
   - Go to **Channels**:
     - Preferred: **Microsoft Teams** → enable and add to a team or chat.  
     - Alternative: **Demo Web App** → enable and copy the URL.  
   - For the demo app, **disable authentication** for lab testing.

7. **Test End-to-End**
   - Ask cross-domain queries such as:
     - `What is the HR leave encashment policy?`
     - `How do I submit an expense report and what’s the approval SLA?`
     - `I forgot my password—what’s the IT reset flow?`
     - `Which documents are needed for vendor onboarding (Finance)?`
   - Verify that responses are sourced from your SharePoint/Excel knowledge.

## Success Criteria

- The Copilot answers **HR/Finance/IT** FAQs grounded in your knowledge sources.  
- “Respond only with selected sources” is enabled, and fallback messaging works.  
- The agent is **published** (Teams or Demo Web App) and accessible for testing.

## Additional Resources

- Microsoft Copilot Studio Documentation  
- Add knowledge with **Generative Answers**  
- Connect **SharePoint** as a knowledge source  
- Authoring tips for topics, trigger phrases, and fallback handling

## Conclusion

You’ve created the **Unified Enterprise Copilot (Foundation)**—a single conversational surface that answers curated HR, Finance, and IT FAQs from trusted content. In **Challenge 2**, you’ll connect **Dataverse** and **Power Automate** for secure, authenticated data access and unified cross-department queries.