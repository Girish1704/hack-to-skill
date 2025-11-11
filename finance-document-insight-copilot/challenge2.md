# Challenge 2: Integrate Document Intelligence and Automate Financial Workflows

## Problem Statement

Finance departments rely on accuracy and speed for document handling, but manual invoice processing and expense validation are time-consuming and error-prone. In this challenge, you’ll integrate **Azure Document Intelligence** and **Power Automate** to automatically extract key financial fields from invoices, validate them, and trigger approval workflows.  

This stage moves the Finance Copilot from static retrieval to automated extraction and workflow orchestration.

## Goals

- Use **Azure Document Intelligence** to extract invoice data (amounts, tax, supplier, dates).  
- Automate financial validation and approval using **Power Automate**.  
- Store structured data in **Dataverse** or **Excel** for analytics and dashboard integration.

## Datasets

- Use the dataset available in `C:\datasets\invoices_sample_set.pdf`.  
- This dataset includes sample invoices and financial forms for testing extraction workflows.  
- You’ll also store extracted data as structured entries in **Dataverse** or Excel.

## Challenge Objectives

1. **Azure Document Intelligence Setup**
   - In the Azure Portal, create a new **Azure AI Document Intelligence** resource named `finance-docintel`.  
   - Under **Studio**, open **Custom Extraction Projects** and upload sample invoices from `C:\datasets\invoices_sample_set.pdf`.  
   - Train a custom model to recognize key fields:  
     - `Invoice ID`, `Vendor Name`, `Date`, `Subtotal`, `Tax`, `Total`, `Payment Terms`.  
   - Once trained, **publish** the model to generate an endpoint and API key.  
   - Test the model using the **Analyze** option in Document Intelligence Studio to confirm accurate field extraction.

2. **Azure Function for Extraction**
   - Create an **Azure Function App** named `finance-extraction-func`.  
   - Use an **HTTP trigger** that:  
     - Accepts uploaded documents from Copilot or Power Automate.  
     - Calls the **Document Intelligence endpoint** for field extraction.  
     - Returns parsed results (JSON format) containing key-value pairs.  
   - Secure the endpoint with a managed identity or API key configuration.  
   - Test using Postman or cURL with a sample document payload.

3. **Power Automate Integration**
   - Create a **Power Automate Flow** named `InvoiceApprovalFlow`.  
   - Add triggers and actions:  
     - **Trigger:** When a document is uploaded to SharePoint or submitted through Copilot.  
     - **Action 1:** Call the Azure Function (`finance-extraction-func`) to extract data.  
     - **Action 2:** Parse and save extracted data to **Dataverse** or **Excel** (fields: Vendor, Amount, Tax, Total, Date).  
     - **Action 3:** Generate an **adaptive approval card** in Teams for the finance manager.  
     - **Action 4:** Upon approval, mark the record as “Approved” and notify the requestor in Teams.  
   - Test the flow by uploading an invoice and confirming end-to-end automation.

4. **Copilot Studio Configuration**
   - In **Copilot Studio**, create a topic named **InvoiceAutomation**.  
   - Add trigger phrases such as:  
     - “Submit a new invoice for processing.”  
     - “Validate invoice totals automatically.”  
     - “Send this invoice for manager approval.”  
   - Add an **Action Node** to call your Power Automate flow and pass document details.  
   - Configure the response node to summarize extracted fields for user confirmation before submission.

5. **Validation**
   - Test the full automation by uploading an invoice PDF.  
   - Verify that:  
     - The invoice is parsed correctly by Document Intelligence.  
     - Extracted fields appear in Dataverse/Excel.  
     - Teams approval card is triggered.  
     - Approval response updates the status accordingly.

## Success Criteria

- Document Intelligence extracts and returns correct invoice fields.  
- Power Automate creates, routes, and updates approval workflows.  
- Copilot Studio successfully interacts with the automated flow.  
- Extracted data is stored in structured form (Excel/Dataverse).  
- Teams notifications for approvals and updates function seamlessly.

## Additional Resources

- [Azure AI Document Intelligence](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/)  
- [Power Automate Approvals Overview](https://learn.microsoft.com/en-us/power-automate/get-started)  
- [Azure Function HTTP Triggers](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook-trigger)  
- [Integrate Copilot Studio with Power Automate](https://learn.microsoft.com/en-us/microsoft-copilot-studio/authoring-connectors)

## Conclusion

You have now enabled **automation and workflow integration** for the Finance Insight Copilot.  
The assistant can automatically extract invoice fields, validate them, route approvals, and store data for analytics—laying the groundwork for an intelligent finance automation system that improves accuracy, speed, and governance.