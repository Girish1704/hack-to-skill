# Challenge 2: Integrate Enterprise Systems with Power Automate and Dataverse for Unified Access

## Problem Statement

Most enterprises operate in silos, with HR, IT, and Finance teams using separate applications and databases. Without unified integration, employees spend time switching between tools, manually sharing data, and duplicating tasks. In this challenge, you’ll connect **Power Automate**, **Dataverse**, and **Copilot Studio** to unify data access across departments—laying the foundation for secure, cross-domain collaboration.

## Goals

- Integrate data from HR, IT, and Finance systems using Power Automate and Dataverse.  
- Enable secure, authenticated queries and cross-domain data retrieval.  
- Allow the Copilot to access and update department data via Dataverse actions.

## Datasets  

- Use the prepared sample data located in `C:\datasets\`:
  - `hr_employees.xlsx` (HR employee data)
  - `finance_invoices.xlsx` (Finance transaction records)
  - `it_tickets.xlsx` (IT support logs)

These will be imported into Dataverse to simulate multi-department datasets.

## Challenge Objectives  

1. **Dataverse Table Setup**
   - Open **Power Apps** → **Dataverse** → **Tables**.
   - Create three tables to represent core departments:
     - **HR_Employees**
       - `EmployeeID` (Text)
       - `Name` (Text)
       - `Department` (Text)
       - `Status` (Choice: Active, Inactive)
       - `LeaveBalance` (Decimal)
     - **Finance_Invoices**
       - `InvoiceID` (Text)
       - `VendorName` (Text)
       - `Amount` (Currency)
       - `Status` (Choice: Pending, Approved, Paid)
       - `IssuedDate` (Date)
     - **IT_Tickets**
       - `TicketID` (Text)
       - `IssueType` (Choice: Hardware, Software, Network, Other)
       - `Status` (Choice: Open, Assigned, Resolved)
       - `RaisedBy` (Text)
       - `DepartmentAffected` (Text)
   - Import data from the provided Excel files into each respective table using **Data → Get Data → Excel**.

2. **Power Automate Integration**
   - Open **Power Automate** and create three **Cloud Flows**:
     1. **GetHRDataFlow**
        - Trigger: **When an HTTP request is received**.
        - Action: **List rows** from the **HR_Employees** table.
        - Filter: Based on query parameters (e.g., Department = 'Finance').
     2. **GetFinanceDataFlow**
        - Trigger: HTTP request.
        - Action: **List rows** from the **Finance_Invoices** table.
        - Return active invoices or unpaid vendors as JSON.
     3. **GetITTicketsFlow**
        - Trigger: HTTP request.
        - Action: **List rows** from the **IT_Tickets** table.
        - Return open or unresolved tickets.
   - Test each flow endpoint using Postman and copy the **HTTP URLs**.

3. **Secure Data Access**
   - Go to **Azure Active Directory** → **App Registrations**.
   - Register an app named `UnifiedCopilot-App`.
   - Assign necessary API permissions for **Power Automate**, **Dataverse**, and **Microsoft Graph**.
   - Generate a **Client Secret** and configure these credentials in your flows for secure communication.
   - Enable role-based access in Dataverse for departmental admins (HR, Finance, IT).

4. **Copilot Studio Integration**
   - In **Copilot Studio**, open your agent created in Stage 1.
   - Add new topics for each department:
     - **Topic: HR Data Query**
       - Trigger phrases:
         - `Show HR employees in Finance department`
         - `List all active employees`
       - Add an **Action Node** calling the `GetHRDataFlow` endpoint.
     - **Topic: Finance Data Query**
       - Trigger phrases:
         - `Show pending invoices`
         - `List vendors with unpaid bills`
       - Call the `GetFinanceDataFlow` endpoint.
     - **Topic: IT Ticket Query**
       - Trigger phrases:
         - `List unresolved IT tickets`
         - `Which tickets are impacting Finance?`
       - Call the `GetITTicketsFlow` endpoint.
   - Parse and present results in a clean, conversational message using data binding (table or bullet list format).

5. **Cross-Domain Query Example**
   - Create an additional **Topic** named **CrossDepartmentInsight**.
   - Trigger phrase: `List IT tickets affecting Finance.`
   - Combine results by chaining calls to both **IT_Tickets** and **Finance_Invoices** flows using conditional logic or Azure Function orchestration.
   - Display unified output like:
     > “There are 3 unresolved IT tickets affecting Finance operations, with total invoice delays of $42,000.”

6. **Testing**
   - In Copilot chat, try:
     - `Show open IT tickets.`
     - `Show all Finance invoices pending approval.`
     - `List employees in Finance department.`
     - `Which IT issues are impacting Finance?`
   - Confirm that the agent retrieves data securely and cross-domain queries work as expected.

## Success Criteria  

- Copilot can retrieve and display data from HR, IT, and Finance through Dataverse.  
- Secure access and authentication are enforced via Azure AD.  
- Power Automate flows respond correctly to queries and return JSON payloads.  
- Cross-domain insights (e.g., IT issues impacting Finance) are produced accurately.

## Additional Resources

- [Power Automate HTTP Trigger Setup](https://learn.microsoft.com/en-us/power-automate/http-connectors)
- [Dataverse Tables Overview](https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-tables-overview)
- [Copilot Studio and Power Automate Integration](https://learn.microsoft.com/en-us/microsoft-copilot-studio/power-automate-integration)
- [Azure AD App Registration Quickstart](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app)

## Conclusion  

You’ve successfully connected HR, IT, and Finance data sources into a single unified backend. The **Unified Enterprise Copilot** can now query multiple systems through Dataverse and Power Automate while maintaining secure access. In the next challenge, you’ll bring in **Azure AI Foundry** and **AI Search** for cross-domain reasoning, enabling the Copilot to answer complex analytical questions across the enterprise.