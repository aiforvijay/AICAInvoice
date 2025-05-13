Invoice Generation Tool for AICA Faculties

Overview

This HTML-based tool is designed to help AICA (AI in ICAI) faculties generate professional invoices for their services. It allows for detailed input of invoice information, batch configurations, and automatic calculation of amounts and taxes. The tool also features a preview mode, PDF generation, an option to update records to a Google Sheet, and local record keeping with Excel export functionality.

Features

* User-Friendly Interface: Data entry is organized into collapsible sections for ease of use.
* Dynamic Batch Configuration: Add multiple batches with multiple line items per batch.
* GST Calculation: Option to include or exclude GST (currently fixed at 9% CGST + 9% SGST if applicable).
* Automatic Calculations:
    * Total taxable amount.
    * CGST and SGST amounts (per batch and overall).
    * Total invoice value.
    * Amounts converted to words.
* Invoice Preview: See a live preview of the invoice as you fill in the details.
* PDF Generation: Generate a downloadable PDF of the invoice.
* Record Keeping:
    * Local Records Tab: View a table of generated invoices (batch-wise).
    * Google Sheets Integration: Option to send invoice data (batch-wise) to a predefined Google Apps Script URL.
    * Excel Export: Download the locally stored invoice records as an `.xlsx` file.
* Default Values: Pre-filled common details (e.g., Faculty Name, Bank Details, Branch Name) to speed up invoice creation, which can be edited as needed.
* Responsive Design: The tool is designed to be usable on various screen sizes, though primarily for desktop use.

How to Use

1.  Open the HTML File:
    * Download the `invoice_tool_updated_v2.html` (or the latest version) file.
    * Open this file directly in a modern web browser (e.g., Chrome, Firefox, Edge, Safari). No web server is required for basic functionality.

2.  Navigate Tabs:
    * Invoice Generation Tab: This is the main tab for creating new invoices. It's active by default.
    * Invoice Records Tab: This tab displays a list of invoices that have been processed using the "Update Records & View" button.

3.  Fill in Invoice Details (Invoice Generation Tab):
    * The input fields are grouped into collapsible sections. Click on a section header to expand or collapse it. Only one section can be open at a time.
    * Invoice & Faculty Details:
        * `Invoice No`: Enter a unique invoice number (default: KVS-).
        * `Invoice Date`: Select the invoice date (defaults to today).
        * `Faculty Name`: Enter the faculty's name (default: K VIJAY SRINIVAS).
    * GST Applicability:
        * Select "Yes" or "No" for GST. This affects tax calculations.
    * Batch Configuration:
        * `Number of Batches`: Enter the number of batches for this invoice.
        * For each batch:
            * `Batch Number`: Enter the batch number (e.g., 325).
            * `Branch Name`: Enter the branch name (default: Hyderabad).
            * Line Items:
                * `Particulars`: Select from the dropdown (e.g., "Session Fees", "Conveyance").
                * `HSN/SAC`: Defaults to 9982 (can be made editable if needed by modifying HTML).
                * `GST Rate`: Auto-filled based on GST applicability.
                * `Amount`: Enter the amount for this line item.
                * Use the `+ Add Item` button to add more line items to a batch.
                * Use the `–` button to remove a line item.
    * Amounts & Taxes (Auto-calculated): These fields are read-only and will be populated when you click "Show Preview."
        * `Total Amount (in words)`
        * `Advance Paid (₹)`: You can enter any advance payment received here.
        * `Total Tax (in words)`
    * Bank Details:
        * Review and edit the default bank details if necessary.

4.  Generate Preview:
    * After filling in the necessary details, click the "Show Preview" button.
    * The invoice preview will appear at the bottom of the "Invoice Generation" tab. This also calculates and populates the "Amounts & Taxes" fields.

5.  Update Records & View (Optional but Recommended for Tracking):
    * Click the "Update Records & View" button.
    * This action will:
        * Send the invoice data (for each batch) to the configured Google Apps Script URL (requires an internet connection).
        * Add the invoice data to a local list.
        * Automatically switch you to the "Invoice Records" tab to see the updated list.

6.  Generate PDF:
    * Ensure you have clicked "Show Preview" first.
    * Click the "Generate PDF" button.
    * The invoice (based on the preview) will be generated as a PDF file and downloaded by your browser.

7.  View Invoice Records (Invoice Records Tab):
    * This tab lists all invoices (batch-wise) that have been processed via "Update Records & View".
    * It includes fixed columns (Invoice No, Date, Batch No, Branch Name, Batch Totals) and dynamic columns based on the "Particulars" entered for batch items.
    * Delete (Local): You can delete records from this local list. This does *not* delete them from the Google Sheet.
    * Download Records (Excel): Click this button to download all records currently displayed in the "Invoice Records" tab as an `.xlsx` file.

Dependencies

The tool uses the following external JavaScript libraries, which are loaded via CDN:

* html2pdf.js (v0.10.1): For generating PDF documents from HTML content.
    * `https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js`
* xlsx.js (SheetJS) (v0.18.5): For generating Excel (`.xlsx`) files.
    * `https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js`

An internet connection is required for these libraries to load and for the Google Sheets integration to work.

Google Sheets Integration

* The "Update Records & View" button sends data to a specific Google Apps Script URL:
    `https://script.google.com/macros/s/AKfycbw8vqPIT_7JfYlWQ9NG-QeXwlFFk3sNFm4lKE07vIjCEr7KbZBnRBw4wzvO5w52qWUpaw/exec`
* This script is responsible for receiving the data and writing it to a Google Sheet.
* Ensure the target Google Sheet is set up correctly to receive the columns: `InvoiceNo`, `InvoiceDate`, `BatchNo`, `BranchName`, `TaxableValue`, `CGSTAmount`, `SGSTAmount`, `TotalValue`.
* If the Google Apps Script URL changes or the sheet structure is modified, the HTML code (specifically the `appScriptUrl` variable in the JavaScript section) might need to be updated.

Customization Notes

* Default Values: Default values for fields like Invoice No, Faculty Name, Branch Name, and Bank Details are set directly in the HTML `value` attributes of the input fields. These can be changed as needed.
* GST Rate: The GST rate is currently hardcoded at 9% CGST and 9% SGST in the JavaScript logic. If this needs to be variable, the JavaScript functions `gstYes()` and `generateInvoiceDataAndPreview()` would need modification.
* HSN/SAC Code: The HSN/SAC code for batch items defaults to "9982". This can be changed in the `renderBatches` function or by making the input field editable.
* Particulars Dropdown: The list of items in the "Particulars" dropdown is defined in the `renderBatches` function within the HTML structure for the select element.

Troubleshooting

* PDF Not Generating Correctly:
    * Ensure you click "Show Preview" before "Generate PDF."
    * Check your internet connection, as `html2pdf.js` is loaded externally.
    * Complex layouts or very long content can sometimes pose challenges for HTML-to-PDF conversion. The tool attempts to optimize for A4 portrait.
* Records Not Updating in Google Sheets:
    * Verify your internet connection.
    * Ensure the `appScriptUrl` in the JavaScript is correct and the Google Apps Script is deployed and has the necessary permissions to write to the target sheet.
    * Check the browser's developer console (usually F12) for any error messages during the fetch request.
* Excel Download Not Working:
    * Check your internet connection for the `xlsx.js` library.
    * Ensure there are records in the "Invoice Records" tab.
