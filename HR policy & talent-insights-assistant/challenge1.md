# Challenge 1: Build a Foundational HR Policy Copilot Agent using Microsoft Copilot Studio# Challenge: Build an HR Policy Copilot with Copilot Studio (SharePoint Knowledge)

## Problem Statement## Problem Statement

HR departments manage thousands of policy documents, FAQs, and benefits information scattered across emails and files. Employees face delays in finding accurate policy information leading to repeated questions and inconsistent guidance. This challenge focuses on building the foundation of an AI-powered HR Policy Assistant capable of answering employee queries using a centralized knowledge base.HR teams handle hundreds of policy docs, benefits FAQs, and leave rules. Employees struggle to find clear answers quickly, leading to repeated questions and inconsistent guidance. In this foundation stage, you’ll build a Copilot Studio assistant that can answer policy questions by using **SharePoint** as the knowledge base.

## Goals## Goals

- Create a Microsoft Copilot Studio agent capable of answering HR policy related FAQs.- Create a Copilot Studio agent for HR policy Q&A.

- Connect it with a local dataset (Excel) that contains HR policies, leave rules, and benefits information.- Connect SharePoint pages/libraries as the assistant’s knowledge.

- Publish the Copilot as a web app and test sample queries.- Publish the Copilot as a web app and test common HR queries.

## Datasets  ## Datasets / Prerequisites

- Use the pre-provided dataset located in `C:\datasets\hr_policies.xlsx`.- **Do not upload any files from the lab VM.**  

- This dataset contains HR policies including remote work guidelines, leave policies, benefits information, and employee FAQs.- Use an existing SharePoint site in your tenant (e.g., **HR Hub**) or create a simple site with a few sample policy pages (Remote Work, Leave & Holidays, Benefits Overview).  

- Optional sample text is available locally at `C:\datasets\hr_policies_samples\` for **copy-paste only** (no file uploads).

## Challenge Objectives  

## Challenge Objectives

1. **Copilot Studio Access and Environment Setup**

   - Navigate to Power Platform portal and create a `developer` environment.1. **Copilot Studio: Environment & Agent**

   - Login to Microsoft Copilot Studio portal and select the developer environment which is created earlier.   - Open **Microsoft Copilot Studio**.

   - Click **+ New agent** and name it **HRInsights-Foundation** (Category: HR).

2. **Create a New Copilot Agent**   - Keep default language/region.

   - Click **+ New Agent**.

   - Name your agent: **HRInsights-Foundation**.2. **Prepare SharePoint Knowledge**

   - Choose the HR category and proceed with default language and region.   - In SharePoint, ensure at least 3 pages exist with short content:

     - **Remote Work Policy** (eligibility, working hours, equipment reimbursement)

3. **Topic Creation**     - **Leave & Holidays** (annual leave, sick leave, public holidays)

   - Add a new topic named **PolicyFAQs**.     - **Benefits Overview** (health insurance, EAP, learning budget)

   - Set trigger phrases such as:   - Tip: You may **copy small snippets** from `C:\datasets\hr_policies_samples\` into SharePoint pages (do **not** upload files).

     - `What is our remote work policy?`

     - `How much annual leave do I have?`3. **Connect SharePoint as Knowledge**

     - `What benefits are included?`   - In Copilot Studio, open your agent → **Knowledge** → **Add data source**.

     - `Explain the sick leave policy`   - Choose **SharePoint** and connect the **HR** site (pages/doc libraries).

   - Add message nodes for sample responses.   - Restrict to the HR policy pages you created/curated.

   - Set scope to **Only from this knowledge** to avoid web fallbacks.

4. **Knowledge Source Integration**

   - From the **Knowledge** section, choose **Add data source**.4. **Topic Creation for FAQs**

   - Upload or connect the Excel file from `C:\datasets\hr_policies.xlsx`.   - Create a topic named **Policy-FAQs**.

   - Select relevant columns as the question and answer fields.   - Add trigger phrases:

   - Set scope to **Only from this knowledge** to avoid web fallbacks.     - `What is our remote work policy?`

     - `How much annual leave do I have?`

5. **Testing the Agent**     - `What benefits are included?`

   - Use the built-in **Test Chat** panel in Copilot Studio.   - Add a **Generative Answers** node configured to use **Knowledge** (SharePoint).

   - Test queries such as:

     - `What's the new remote-work policy?`5. **Test the Agent**

     - `How many sick days do we get?`   - In **Test** pane, try:

     - `Summarize benefits for new hires.`     - `What’s the new remote-work policy?`

     - `How many sick days do we get?`

6. **Publishing the Agent**     - `Summarize benefits for new hires.`

   - Navigate to **Settings → Channels**.

   - Enable **Demo Web App** channel.6. **Publish as Web App**

   - Disable authentication for ease of access.   - Go to **Channels** → enable **Demo Web App**.

   - Publish and test the agent in the browser.   - (For lab purposes) Disable authentication.

    - Publish and open the web URL to verify.

## Success Criteria   

## Success Criteria

- The agent successfully responds to HR policy queries using the dataset.

- The web app is accessible without authentication.- Agent answers policy questions using **SharePoint** content only.

- Validation passes successfully.- Demo Web App is accessible and returns consistent answers.

- Validation step succeeds.

## Additional Resources

## Additional Resources

- [Microsoft Copilot Studio Documentation](https://learn.microsoft.com/en-us/microsoft-copilot-studio/)

- [Connect knowledge sources in Copilot Studio](https://learn.microsoft.com/en-us/microsoft-copilot-studio/knowledge)- Microsoft Copilot Studio Documentation  

  - Copilot Studio Knowledge Sources  

## Conclusion  - SharePoint Pages Basics

You have built the foundational layer of the HR Policy Copilot that can answer FAQs intelligently using Copilot Studio. In the next challenge, you'll integrate Power Automate for feedback collection and compliance reminders.## Conclusion

You’ve built a foundational **HR Policy Copilot** that uses SharePoint as a trusted knowledge base. Next, you’ll extend the assistant with **Power Automate** to collect feedback, create clarification requests, and send compliance reminders.