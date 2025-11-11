# Challenge 2: Integrate Multi-Channel Feedback Analysis and Automation using Power Automate and Logic Apps
  
## Problem Statement

Collecting customer feedback is only the first step — organizations need seamless integration and automation to extract value from it. In this challenge, you’ll integrate Power Automate and Logic Apps with Copilot Studio to ingest multi-channel feedback, run sentiment analysis with Azure AI Language Services, and automate alerts and data storage in Dataverse.

## Goals

- Integrate feedback collection from multiple sources using Logic Apps and Power Automate.
- Apply sentiment analysis using Azure AI Language Services.
- Automate feedback logging, escalation, and sentiment alerts within Dataverse and Teams.

## Datasets  

- Use the sample dataset located in `C:\datasets\customer_feedback_sample.csv` to simulate feedback data collected from multiple channels (Email, Web Form, Survey).  
- This dataset will help you verify ingestion and sentiment analysis flows.

## Challenge Objectives  

1. **Power Automate Setup**
   - Open **Power Automate** from Microsoft 365 Apps.
   - Create a new **Cloud Flow** named `ProcessCustomerFeedbackFlow`.
   - Trigger: **Manually trigger a flow** (for testing) or **When a new email arrives** (for production simulation).
   - Add parameters for:
     - `CustomerName`
     - `Channel`
     - `FeedbackText`
     - `DateReceived`

2. **Dataverse Table Creation**
   - In your environment, create a new **Dataverse** table called `CustomerFeedback`.
   - Define the following columns:
     - `CustomerName` (Text)
     - `Channel` (Choice)
     - `FeedbackText` (Multiline Text)
     - `Sentiment` (Choice: Positive, Neutral, Negative)
     - `SentimentScore` (Decimal)
     - `DateReceived` (DateTime)
   - Save and publish the table schema.

3. **Azure AI Language Service Integration**
   - In the Azure portal, create a **Language Service** resource named `CustomerSentimentLangService`.
   - Under **Features**, enable **Sentiment Analysis** and **Key Phrase Extraction**.
   - Copy the **endpoint** and **API key**.
   - In your Power Automate flow:
     - Add an **HTTP action** to call the Language API.
     - Use the endpoint `/text/analytics/v3.1/sentiment`.
     - Pass `FeedbackText` as the input body.
     - Parse the response to extract `Sentiment` and `ConfidenceScore`.

4. **Logic App Integration (Optional Enhancement)**
   - In the Azure portal, create a **Logic App** named `IngestCustomerFeedback`.
   - Add connectors for:
     - **Outlook / Exchange** (read new emails with subject “Customer Feedback”)
     - **Microsoft Forms / Survey** (for survey submissions)
     - **Social Media Connector** (for public mentions)
   - Use a **Data Operations** step to clean and merge all incoming feedback into a consistent schema.
   - Call Power Automate Flow (`ProcessCustomerFeedbackFlow`) via an HTTP trigger to send merged feedback data for processing.

5. **Feedback Automation and Alerts**
   - Back in **Power Automate**, after the sentiment is computed:
     - Add a step to **Insert a row** into the Dataverse `CustomerFeedback` table.
     - If sentiment = **Negative** and score < 0.4:
       - Add a **Condition** branch to send a **Teams notification** to the CX Manager channel.
       - Include feedback details, channel, and timestamp.
   - Test with multiple entries and validate that alerts fire correctly.

6. **Copilot Studio Integration**
   - In **Copilot Studio**, open your existing agent and navigate to **Actions**.
   - Add the Power Automate flow `ProcessCustomerFeedbackFlow` as a callable action.
   - Create a new topic named **FeedbackCollector** with trigger phrases such as:
     - `Submit my feedback`
     - `I want to share my experience`
     - `Report an issue about the service`
   - Configure fields for `CustomerName`, `Channel`, and `FeedbackText`.
   - Call the Power Automate flow action and show confirmation messages in chat.

7. **Testing**
   - Interact with Copilot using sample phrases like:
     - `I want to give feedback about delayed responses.`
     - `Submit a new feedback from survey data.`
   - Confirm that sentiment analysis, alerts, and Dataverse entries work end-to-end.

## Success Criteria  

- Copilot successfully triggers Power Automate and Logic App workflows.
- Sentiment is analyzed correctly via Azure AI Language Service.
- Negative feedback automatically triggers alerts in Teams.
- All feedback records are logged in Dataverse with accurate sentiment labels.

## Additional Resources

- [Azure AI Language Documentation](https://learn.microsoft.com/en-us/azure/ai-services/language-service/overview)
- [Integrate Power Automate with Copilot Studio](https://learn.microsoft.com/en-us/microsoft-copilot-studio/power-automate-integration)
- [Logic Apps Connectors Overview](https://learn.microsoft.com/en-us/azure/connectors/apis-list)
- [Dataverse Tables Quickstart](https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-tables-overview)

## Conclusion  

You have successfully integrated **Power Automate**, **Logic Apps**, and **Azure AI Language Service** to automate sentiment-based workflows. Your Copilot can now collect feedback, analyze tone and sentiment, and notify teams for quick action — creating a proactive, data-driven customer experience ecosystem.