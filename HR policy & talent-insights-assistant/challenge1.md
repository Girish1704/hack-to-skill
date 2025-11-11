# Challenge: Build an HR Policy Copilot with Copilot Studio (SharePoint Knowledge)
  
## Problem Statement

HR teams handle hundreds of policy docs, benefits FAQs, and leave rules. Employees struggle to find clear answers quickly, leading to repeated questions and inconsistent guidance. In this foundation stage, you’ll build a Copilot Studio assistant that can answer policy questions by using **SharePoint** as the knowledge base.

## Goals

- Create a Copilot Studio agent for HR policy Q&A.
- Connect SharePoint pages/libraries as the assistant’s knowledge.
- Publish the Copilot as a web app and test common HR queries.

## Datasets / Prerequisites

- **Do not upload any files from the lab VM.**  
- Use an existing SharePoint site in your tenant (e.g., **HR Hub**) or create a simple site with a few sample policy pages (Remote Work, Leave & Holidays, Benefits Overview).  
- Optional sample text is available locally at `C:\datasets\hr_policies_samples\` for **copy-paste only** (no file uploads).

## Challenge Objectives

1. **Copilot Studio: Environment & Agent**
   - Open **Microsoft Copilot Studio**.
   - Click **+ New agent** and name it **HRInsights-Foundation** (Category: HR).
   - Keep default language/region.

2. **Prepare SharePoint Knowledge**
   - In SharePoint, ensure at least 3 pages exist with short content:
     - **Remote Work Policy** (eligibility, working hours, equipment reimbursement)
     - **Leave & Holidays** (annual leave, sick leave, public holidays)
     - **Benefits Overview** (health insurance, EAP, learning budget)
   - Tip: You may **copy small snippets** from `C:\datasets\hr_policies_samples\` into SharePoint pages (do **not** upload files).

3. **Connect SharePoint as Knowledge**
   - In Copilot Studio, open your agent → **Knowledge** → **Add data source**.
   - Choose **SharePoint** and connect the **HR** site (pages/doc libraries).
   - Restrict to the HR policy pages you created/curated.
   - Set scope to **Only from this knowledge** to avoid web fallbacks.

4. **Topic Creation for FAQs**
   - Create a topic named **Policy-FAQs**.
   - Add trigger phrases:
     - `What is our remote work policy?`
     - `How much annual leave do I have?`
     - `What benefits are included?`
   - Add a **Generative Answers** node configured to use **Knowledge** (SharePoint).

5. **Test the Agent**
   - In **Test** pane, try:
     - `What’s the new remote-work policy?`
     - `How many sick days do we get?`
     - `Summarize benefits for new hires.`

6. **Publish as Web App**
   - Go to **Channels** → enable **Demo Web App**.
   - (For lab purposes) Disable authentication.
   - Publish and open the web URL to verify.
 
## Success Criteria

- Agent answers policy questions using **SharePoint** content only.
- Demo Web App is accessible and returns consistent answers.
- Validation step succeeds.

## Additional Resources

- Microsoft Copilot Studio Documentation  
- Copilot Studio Knowledge Sources  
- SharePoint Pages Basics

## Conclusion

You’ve built a foundational **HR Policy Copilot** that uses SharePoint as a trusted knowledge base. Next, you’ll extend the assistant with **Power Automate** to collect feedback, create clarification requests, and send compliance reminders.