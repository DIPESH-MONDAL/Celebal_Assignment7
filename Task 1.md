# ASSIGNMENT 1

Let's suppose you have 3 different types of file 
1) `CUST_MSTR_20191112.csv` 
2) `master_child_export-20191112.csv` 
3) `H_ECOM_ORDER.csv` 

All these files will be in the data lake container You have to fetch all three types of files into their respective folders. 

**Note**: There could be multiple files on all 3 types for different dates for example `CUST_MSTR_20191112.csv` and `CUST_MSTR_20191113.csv `

1) For the "`CUST_MSTR`" starting name of the file You have to create an additional column for a date that will fetch the data value from the filename and put it into an additional column Date format: 2019-11-12 and load it into the "`CUST_MSTR`" table 
2) For the "`master_child_export`" starting name of the file You have to create two additional columns date and date key which will fetch the data from the filename and put it into the additional columns. 
    - Date format: 2019-11-12 
    - DateKey format: 20191112 

    and load it into the "`master_child`" table 
3) for the "`H_ECOM_ORDER`" type of file you have to load it into the database as it is. and load it into "`H_ECOM_Orders`" table 

**Note**: This process will work on truncate load on a daily basis


**Resources :**
https://drive.google.com/drive/folders/1jtasnqX7BnmPfDKEWx2WBmDlN20el1AE?usp=drive_link


## Answer

Reference : ChatGPT and Bard (Unable to create Azure account)

1. Set Up Data Lake Storage and SQL Database:
        
    - Set up an Azure SQL Database with tables: `CUST_MSTR`, `master_child`, and `H_ECOM_Orders`.

2. Create an ADF Pipeline:
    - In the Azure portal, navigate to your Data Factory instance and open it.
    - Create a new pipeline.

3. Create Linked Services
    - Create Linked Service for Azure SQL Database:
        In the same "Manage" tab, create a new Linked Service for your Azure SQL Database.

4. Create Datasets

    - Create Dataset for ADLS Input Files:
        Create datasets for each type of file (CUST_MSTR, master_child_export, H_ECOM_ORDER).

    - Create Dataset for Azure SQL Database Tables:
        Create datasets for the CUST_MSTR, master_child, and H_ECOM_Orders tables in the SQL Database.

5. Create Pipelines
    1. Pipeline for CUST_MSTR Files

        - Get Metadata Activity:
        Use the Get Metadata activity to get the list of files in the ADLS container.

        - ForEach Activity:
        Use the ForEach activity to iterate over the list of files.
        Inside the ForEach, add a Filter activity to filter files that start with CUST_MSTR.

        - Copy Data Activity:
        Use the Copy Data activity to copy data from the filtered file to the SQL table.
        In the Source settings, use the file name to extract the date and add it as a column using Data Flow.

    2. Pipeline for master_child_export Files

        - Get Metadata Activity:
        Similar to the CUST_MSTR pipeline, get the list of files.

        - ForEach Activity:
        Use the ForEach activity to iterate over the list of files.
        Inside the ForEach, add a Filter activity to filter files that start with master_child_export.

        - Copy Data Activity:
        Use the Copy Data activity to copy data from the filtered file to the SQL table.
        In the Source settings, use the file name to extract the date and date key and add them as columns using Data Flow.

    3. Pipeline for H_ECOM_ORDER Files

        - Get Metadata Activity:
        Similar to the CUST_MSTR pipeline, get the list of files.

        - ForEach Activity:
        Use the ForEach activity to iterate over the list of files.
        Inside the ForEach, add a Filter activity to filter files that start with H_ECOM_ORDER.

        - Copy Data Activity:
        Use the Copy Data activity to copy data from the filtered file to the SQL table as is.

6. Create Data Flow for Adding Columns

    - Create a Data Flow:
        In the Author tab, create a new Data Flow.
        Add a source transformation to read from the respective dataset.
        Add a derived column transformation to add the date or date key column.
        Use the file name to derive the date values.

7. Configure Triggers

    - Create a Schedule Trigger:
        Configure the trigger to run on a daily basis.

Here's an example JSON configuration for a ScheduleTrigger:

```json

{
    "name": "DailyTrigger",
    "properties": {
        "type": "ScheduleTrigger",
        "typeProperties": {
            "recurrence": {
                "frequency": "Day",
                "interval": 1,
                "startTime": "2023-01-01T00:00:00Z",
                "timeZone": "UTC"
            }
        },
        "pipelines": [
            {
                "pipelineReference": {
                    "referenceName": "CUST_MSTR_Pipeline",
                    "type": "PipelineReference"
                }
            },
            {
                "pipelineReference": {
                    "referenceName": "master_child_export_Pipeline",
                    "type": "PipelineReference"
                }
            },
            {
                "pipelineReference": {
                    "referenceName": "H_ECOM_ORDER_Pipeline",
                    "type": "PipelineReference"
                }
            }
        ]
    }
}
```