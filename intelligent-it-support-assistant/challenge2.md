# Challenge 2: Integrate Power Automate Tools within Copilot Studio for IT Ticket Automation
  
## Problem Statement

While your foundational chatbot can answer FAQs, enterprise IT environments also require automated workflows to handle ticketing operations efficiently.  
In this challenge, you will extend your Copilot agent to include ticket automation directly within the Copilot Studio portal using Power Automate connectors and actions.  
You’ll enable the bot to create, update, and escalate IT tickets while sending real-time notifications to support engineers all without leaving Copilot Studio.

## Goals

- Automate IT ticket creation and tracking directly through Copilot Studio’s integrated Power Automate tools.  
- Enable Microsoft Teams–based notifications for support engineers.  
- Store and manage all ticket data within Dataverse in a structured format.

## Datasets  

- Use the pre-provided dataset in `C:\datasets\tickets_template.csv`.  
- This dataset contains sample ticket templates and metadata to simulate user issue tracking.

## Challenge Objectives  

1. **Open Copilot Studio and Access Power Automate Tools**
   - Launch **Microsoft Copilot Studio** from your Microsoft 365 portal.  
   - Open the **ITSupportAssistant-Foundation** agent you created in the previous challenge.  
   - From the left navigation panel, go to **Tools → Power Automate** to view available connectors and builder options.

2. **Create a Dataverse Table for Ticket Management**
   - Within the Copilot Studio environment (Dataverse is automatically provisioned):  
     - Navigate to **Data → Tables → + New Table**.  
     - Name the table **Tickets** and add these columns:
       - `TicketID` (Autonumber)
       - `UserName` (Text)
       - `IssueDescription` (Multiline Text)
       - `Priority` (Choice: Low, Medium, High)
       - `Status` (Choice: Open, In Progress, Resolved)
   - Import sample rows from `C:\datasets\tickets_template.csv` to populate initial ticket data.

3. **Design the Ticket Creation Flow within Copilot Studio**
   - In Copilot Studio, navigate to **Tools → Power Automate → Create Flow**.  
   - Name the flow **CreateSupportTicket**.  
   - Add the following steps:
     1. **Trigger:** Use “When a Copilot topic runs this flow.”  
     2. **Action 1:** Add a **Dataverse → Add a new row** action.  
        - Target table: `Tickets`
        - Map fields from user input (name, issue description, priority).
        - Set default **Status = Open**.  
     3. **Action 2:** Add a **Teams → Post message in a channel** action.  
        - Channel: IT Support Notifications (create if needed).  
        - Message: Include Ticket ID, UserName, and IssueDescription.  

   - Save and test the flow to ensure it successfully adds entries and sends Teams messages.

4. **Integrate the Flow into Your Copilot Agent**
   - In **Copilot Studio → Topics**, create or open a topic named **TicketAutomation**.  
   - Add **Trigger phrases** like:
     - `I want to raise a support ticket`
     - `Report an issue with my device`
     - `Create a ticket for my IT problem`
   - Add a **Power Automate Action Node** to call the **CreateSupportTicket** flow.  
   - Map conversation variables (e.g., username, issue description, priority) to flow parameters.

5. **Test the Copilot Agent**
   - Use the **Test your copilot** panel to simulate conversations such as:
     - `My Outlook keeps crashing, please raise a ticket.`
     - `Create a high-priority ticket for my network issue.`  
   - Verify that the flow executes and a Teams notification is received.

6. **Publish and Validate**
   - Publish your updated agent via the **Demo Web App** channel.  
   - Confirm ticket creation and Teams notifications work seamlessly.  

## Success Criteria  

- The Copilot agent successfully triggers ticket creation flows within the Copilot Studio portal.  
- Tickets appear correctly in the Dataverse table with assigned IDs and “Open” status.  
- Teams notifications are sent automatically when tickets are created.  

## Additional Resources
- [Build flows directly in Copilot Studio](https://learn.microsoft.com/en-us/microsoft-copilot-studio/power-automate-integration)  
- [Work with Dataverse in Copilot Studio](https://learn.microsoft.com/en-us/microsoft-copilot-studio/data-connections)  
- [Send messages to Teams channels using Power Automate](https://learn.microsoft.com/en-us/connectors/teams/)  

## Conclusion  

You have enhanced your Copilot’s functionality by integrating Power Automate connectors **directly within Copilot Studio** to automate IT ticket creation and notifications.  
Your Copilot is now capable of handling real-world service automation without requiring external Power Automate setup — paving the way for adding AI-driven insights and recommendations in the next stage.
