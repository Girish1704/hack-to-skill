# Challenge 1: Build a Finance FAQ & Manual Document Intake Copilot (Foundation)

## Problem Statement

Finance users need a single place to **ask questions** (policies, processes, deadlines) and **submit documents** (invoices, statements) without bouncing between email and shared folders. In this foundation stage, you’ll build a Copilot Studio chatbot that answers **finance FAQs** grounded in SharePoint/Excel content and supports **manual document intake** to a SharePoint invoice library. This creates a unified entry point before you automate extraction in later stages.

## Goals

- Create a Copilot Studio agent that answers **finance FAQs** from curated SharePoint/Excel sources.  
- Enable **manual document upload** (invoice/statement PDFs) routed to a SharePoint repository.  
- Publish the agent to **Teams** (or Demo Web App) for quick access.

## Datasets

- Use sample FAQ and seed files from your lab VM:
  - `C:\datasets\finance_faq.xlsx`  *(two columns: Question, Answer)*  
  - `C:\datasets\invoice_samples.pdf` *(multi-page pdf containing example invoices)*

> If `finance_faq.xlsx` doesn’t exist, create a simple two-column sheet with headers **Question** and **Answer** and save to the same path.

## Challenge Objectives

1. **Prepare SharePoint Knowledge & Repositories**
   - Create a SharePoint site (e.g., **finance-ops**).
   - In **Documents**, add:
     - Folder **/FAQs** → upload `finance_faq.xlsx`. Ensure it’s a **Table** or has a header row.
     - Library **/Invoices** (or use **Invoices** document library). Create columns:
       - `VendorName` (Text), `InvoiceDate` (Date), `Amount` (Number), `Notes` (Multiple lines), `UploadedBy` (Person).
   - (Optional) Create an **Excel tracking workbook** `invoice_intake_log.xlsx` with columns that mirror the library fields for quick tabular review.

2. **Create the Copilot Agent**
   - Open **Microsoft Copilot Studio** → **+ New agent**.  
   - Name: **FinanceInsight-Foundation** (Category: Finance).  
   - Create with default language/region.

3. **Add Knowledge via Generative Answers**
   - In the agent, add **Generative Answers** (Knowledge sources).  
   - Select **SharePoint** and point to the **/FAQs** folder.  
   - Enable **Respond only with data from the selected sources** to keep answers grounded.

4. **Topic: Finance FAQs**
   - Create **Topic**: **Finance-FAQ** with trigger phrases:
     - `finance help`, `expense policy`, `invoice deadline`, `reimbursement timeline`, `tax guidelines`
   - Add a **Generative Answers** node targeting your SharePoint knowledge.  
   - Add a fallback message if content isn’t found:  
     > “I couldn’t find that in our current FAQs. Try rephrasing or ask about expenses, reimbursements, taxes, or invoice timelines.”

5. **Topic: Manual Document Intake**
   - Create **Topic**: **Upload-Invoice** with trigger phrases:
     - `submit invoice`, `upload finance document`, `add vendor bill`, `share statement`
   - Collect inputs via **Question** nodes:
     - `VendorName` (Short text)
     - `InvoiceDate` (Date)
     - `Amount` (Number)
     - `Notes` (Long text, optional)
   - Provide **upload instructions** to the user:
     - If using **Teams**: prompt user to attach the PDF in chat (Copilot transcript) or share a link.  
     - If using **Demo Web App**: provide the **SharePoint Invoices** library link and instruct to upload the file, then paste the file URL back.
   - After you capture the file/link, add an **Action** using the **SharePoint connector**:
     - **Create file** in **/Invoices** with a unique name pattern `INV-${yyyyMMdd}-${VendorName}.pdf`.  
     - **Update file properties** (columns) with the collected metadata.
   - Add a **Message** confirming successful intake and echoing a reference (file name or URL).

6. **(Optional) Log to Excel**
   - Add a second **Action** using **Excel Online (Business)** to **Add a row** into `invoice_intake_log.xlsx` with the same metadata and the file link for a simple register.

7. **Channels & Publishing**
   - Go to **Channels**:
     - Preferred: **Microsoft Teams** → enable; add to a team or chat for finance staff.  
     - Alternative: **Demo Web App** → enable and copy URL.  
   - For demo app testing, **disable authentication** if required by your lab.

8. **Test End-to-End**
   - Ask FAQ prompts, for example:
     - `What is the month-end invoice submission deadline?`
     - `How do I claim travel reimbursement?`
   - Try the intake flow:
     - `Submit invoice` → provide VendorName/Date/Amount/Notes → upload PDF → confirm.  
   - Verify:
     - The PDF appears in the **Invoices** library with populated columns.  
     - (Optional) A new row is added to `invoice_intake_log.xlsx`.

## Success Criteria

- Copilot answers finance FAQs grounded in SharePoint/Excel with **Respond only with selected sources** enabled.  
- Manual document intake stores PDFs in the **Invoices** library with metadata (Vendor, Date, Amount, Notes).  
- The agent is **published** (Teams or Demo Web App) and works end-to-end.

## Additional Resources

- Microsoft Copilot Studio Documentation  
- Generative Answers (Add knowledge; SharePoint connector)  
- SharePoint document libraries: custom columns & content types  
- Excel Online (Business) connector for logging rows

## Conclusion

You’ve built the **Finance Document Insight Copilot (Foundation)**—a single conversational surface for finance FAQs and manual document intake to SharePoint. In **Challenge 2**, you’ll integrate **Azure Document Intelligence** and **Power Automate** to automatically extract fields, validate entries, and route approvals.