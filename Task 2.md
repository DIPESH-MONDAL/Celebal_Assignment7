# ASSIGNMENT 2

Let's suppose I have 3 data sources 
1) **Oracle(on-premise)** The monthly Incremental data size will be approx 30 GB and the total table count is 20. 
2) **Salesforce** The monthly Incremental data size will be approx 50 GB and the total table count is 120. 
3) **Semi-structured files on FTP** The monthly data size will be approx 5 GB and the Approximate file count per month will be 20.

Now based on this information make an Azure bill of material and share the Link of the same to your mentor for validation with a detail description.

## Answer

Reference : ChatGPT and https://www.youtube.com/watch?v=rMKmbZ1SYQg

To create an **Azure Bill of Materials (BoM)** and estimate the cost for integrating these data sources into Azure Data Factory, follow these steps:

### Step 1: Identify the Services Required

Based on the provided data sources and requirements, you'll need the following Azure services:

1. **Azure Data Factory (ADF)**: To orchestrate and manage the data integration pipelines.
2. **Azure Storage (Blob Storage)**: To store intermediate and processed data.
3. **Azure SQL Database**: To store the final processed data.
4. **Azure Virtual Network**: To securely connect your on-premise Oracle database to Azure.
5. **Self-hosted Integration Runtime**: To connect to the on-premise Oracle database.
6. **Azure Data Lake Storage**: To store large amounts of semi-structured data from FTP.
7. **Azure Logic Apps**: To handle the data extraction from Salesforce.

### Step 2: Estimate the Resources

### Step 3: Use the Azure Pricing Calculator

1. **Open the Azure Pricing Calculator**:
   - [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)

2. **Add Services to the Calculator**

### Step 4: Configure the Details


### Step 5: Generate the Estimate

1. **Configure each service** in the Azure Pricing Calculator with the details specified above.
2. **Review the pricing** for each service and the total estimated cost.
3. **Export the estimate**:
   - After configuring the services, export the estimate to a PDF or shareable link.

### Step 6: Share the Estimate

1. **Share the Link**:
   - You can use the "Share" feature in the Azure Pricing Calculator to generate a link to the estimate.
   - Send the link to your mentor for validation.


---

### Steps to Generate Azure Pricing Estimate Link

1. Open the [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/).
2. Add and configure the necessary services as detailed above.
3. After configuring all the services, click on the "Export" button to export the estimate as a PDF or shareable link.
4. Send the link or PDF to your mentor for validation.

This detailed process and description will ensure that your mentor has a clear understanding of the Azure resources and estimated costs involved in your project.

According to my estimate and calculation the bill generated is :-

1. [AzureBill-USD](./ExportedEstimate_USD.xlsx)
2. [AzureBill-INR](./ExportedEstimate_INR.xlsx)