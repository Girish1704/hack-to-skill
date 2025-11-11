# Challenge: Integrate Power Automate for Feedback, Clarifications, and Compliance Reminders
  
## Problem Statement

Policy answers alone aren’t enough—HR also needs structured feedback, clarification requests, and automated reminders for compliance or training renewals. In this stage, you’ll integrate **Power Automate** with your Copilot to capture employee inputs and trigger proactive workflows.

## Goals

- Add Power Automate **Agent Flows** to capture policy feedback/clarification requests.
- Store entries in **Dataverse** tables.
- Send **Teams** notifications and scheduled compliance reminders.

## Datasets / Prerequisites

- No uploads from `C:\datasets`.  
- You’ll create lightweight **Dataverse** tables to store records.  
- (Optional) You can reference sample questions from `C:\datasets\hr_feedback_prompts.txt` for test messages (copy-paste only).

## Challenge Objectives

1. **Dataverse Tables**
   - Create a table **PolicyFeedback** with columns:
     - `EmployeeEmail` (Text), `Topic` (Text), `Message` (Multiline Text),
     - `SentimentHint` (Choice: Positive/Neutral/Negative),
     - `CreatedOn` (Date/Time).
   - Create a table **ComplianceTasks** with columns:
     - `EmployeeEmail` (Text), `PolicyName` (Text),
     - `DueOn` (Date), `Status` (Choice: Pending/Done).

2. **Power Automate: Feedback Flow**
   - Create a **Cloud flow** named `SubmitPolicyFeedback`.
   - Trigger: **Power Automate → Copilot (Agent Flow)**.
   - Actions:
     - Add a row in **PolicyFeedback** with Copilot inputs.
     - Post a **Teams** message to the HR channel with an Adaptive Card summary and deep link to the SharePoint policy page.

3. **Power Automate: Clarification Request Flow**
   - Flow name: `RequestPolicyClarification`.
   - Trigger: **Agent Flow**.
   - Actions:
     - Add a row in **PolicyFeedback** (Topic = Clarification).
     - Send an **email** to the HR mailbox with the employee’s question and policy link.
     - Reply token back to Copilot for “ticket created” confirmation.

4. **Power Automate: Compliance Reminder Flow**
   - Flow name: `ComplianceReminders`.
   - Trigger: **Recurrence** (daily).
   - Actions:
     - List rows from **ComplianceTasks** where `Status = Pending` and `DueOn <= utcNow() + 7d`.
     - Send **Teams** proactive message to each employee: reminder with “Acknowledge” button.
     - If user clicks “Acknowledge”, update `Status = Done`.

5. **Wire Up in Copilot Studio**
   - In **Actions**, **Add existing flow** for each of the three flows.
   - Create topics:
     - **Give-Feedback** (inputs: email, topic, free text).
     - **Ask-Clarification** (inputs: email, policy URL or keyword).
     - **Set-Compliance-Task** (inputs: policy name, due date, email).
   - For each topic, call the respective Agent Flow and return a friendly confirmation message.

6. **Test End-to-End**
   - Ask Copilot:
     - `I want to give feedback on the remote work policy.`
     - `Raise a clarification on sick leave eligibility.`
     - `Create a compliance task for Security Awareness by 30 Nov for alex@contoso.com.`

7. **Publish**
   - Publish and confirm Teams messages, emails, and Dataverse rows are created.

## Success Criteria

- Copilot successfully triggers **all three flows**.
- Dataverse entries appear as expected.
- Teams notifications and compliance acknowledgements work.

## Additional Resources

- Copilot Studio + Power Automate Integration  
- Dataverse Tables Overview  
- Teams Adaptive Cards overview

## Conclusion

Your HR Copilot now captures structured **feedback**, **clarification requests**, and automates **compliance reminders**, closing the loop between knowledge discovery and HR operations.