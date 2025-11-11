# Challenge 1: Build a Teams-ready Customer Feedback Copilot with Copilot Studio (Foundation)

## Problem Statement

CX teams need a quick, consistent way to capture structured customer feedback and answer common FAQs directly where users already work—Teams. In this foundation stage, you’ll build a Copilot Studio chatbot that collects feedback (name, channel, rating, comment) and can respond to basic FAQs, all inside Teams.

## Goals

- Create a Copilot Studio agent to capture **structured customer feedback**.
- Add a simple **FAQ** experience for common support questions.
- Publish the Copilot to **Teams** (or Demo Web App) for easy access and testing.

## Datasets

- No uploads are required in this challenge.  
- (Optional) You may copy example FAQ text from `C:\datasets\customer_faq_samples.txt` into your topic messages to seed basic answers.

## Challenge Objectives

1. **Create the Copilot Agent**
   - Open **Microsoft Copilot Studio**.
   - Click **+ New agent** and name it **CustomerFeedback-Foundation** (Category: Customer Experience).
   - Keep the default language/region and create the agent.

2. **Design the Feedback Form (Topic)**
   - Create a new **Topic** named **Collect-Feedback**.
   - Add trigger phrases:
     - `Submit feedback`
     - `Share my experience`
     - `I want to report an issue`
   - Add **Question** nodes to collect:
     - `CustomerName` (Short text)
     - `Channel` (Choices: Email, Web, Chat, Social)
     - `Category` (Choices: Product, Support, Delivery, Billing, Other)
     - `Rating` (Number 1–5)
     - `Comment` (Long text)
   - After capturing values, add a **Message** node summarizing the submission back to the user for confirmation.

3. **Add a Confirmation & Thank-you Flow**
   - Add a **Yes/No** confirmation step:
     - On **Yes** → Show a “Thank you” message and provide a reference ID (use a simple generated string like `FBK-<random 5 digits>` via a variable).
     - On **No** → Loop back to allow the user to edit fields (at least `Rating` and `Comment`).

4. **Create a Basic FAQ Topic**
   - New **Topic**: **Customer-FAQ** with trigger phrases:
     - `FAQs`
     - `How do I contact support?`
     - `Where can I track my order?`
   - Add a **Message** node (or **Generative Answers** if you later connect a knowledge source) with 5–8 concise Q&A entries (contact info, hours, refunds basics, ETA/Tracking steps, escalation path).

5. **Agent Settings & Variables**
   - In **Variables**, create:
     - `FeedbackId` (Text)
     - `SubmissionTime` (DateTime)
   - Set `SubmissionTime` when the form is confirmed; compose `FeedbackId` (e.g., `FBK-${randomNumber()}` via an expression or static placeholder).

6. **Publish to Teams (or Demo Web App)**
   - Navigate to **Channels**:
     - Preferred: **Microsoft Teams** → enable and follow prompts to add to a team or chat.
     - Alternative: **Demo Web App** → enable and copy the URL.
   - (Lab convenience) If using Demo Web App, **disable authentication** for testing.

7. **Test End-to-End**
   - In Teams or Demo Web App, try:
     - `Submit feedback`
     - Provide details for all fields and confirm.
     - Ask `FAQs` and verify the assistant replies with your Q&A content.

## Success Criteria

- Users can **submit structured feedback** (name, channel, category, rating, comment) and receive a confirmation message with a feedback ID.
- The **FAQ topic** responds correctly to common questions.
- The Copilot is **accessible in Teams** (or Demo Web App) and works end-to-end.

## Additional Resources

- Microsoft Copilot Studio Documentation  
- Topics, Variables, and Publishing Channels in Copilot Studio  
- Authoring tips for question/choice nodes and branching

## Conclusion

You’ve built the foundation of the **Customer Feedback & Sentiment Intelligence Copilot**: a Teams-ready assistant that collects structured feedback and answers FAQs. In the next challenge, you’ll integrate **Power Automate** and **Logic Apps** to ingest multi-channel feedback and apply **Azure AI Language** sentiment analysis with Dataverse storage and alerts.