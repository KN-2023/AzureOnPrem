# AzureOnPrem
### Project Architecture

<img width="400" height="200" alt="Corrected Medallion Architecture Diagram" src="https://github.com/user-attachments/assets/65aaae9b-d4b9-4c81-a8bf-67f6ea104dc6" />

- Implements an end-to-end Azure Data Engineering pipeline using Azure Data Factory (ADF) and Azure Data Lake Storage Gen2.
- Ingests data from on-premises CSV files, REST APIs, and Azure SQL Database.
- Uses Self-Hosted Integration Runtime (SHIR) for on-premises data connectivity.
- Stores raw data in the Bronze layer, cleans and transforms it in the Silver layer, and creates business-ready datasets in the Gold layer.
- Uses ADF Mapping Data Flows for data transformation.
- Implements watermark-based incremental loading to process only new or updated records.
- Uses ADF for pipeline orchestration and Azure Logic Apps for failure notifications.
- Uses GitHub and Azure DevOps for repository management and branch-based development workflows.

### Technology Stack

- **Data Integration:** Azure Data Factory
- **Data Storage:** Azure Data Lake Storage Gen2, Azure SQL Database
- **Data Processing:** ADF Mapping Data Flows
- **Connectivity:** Self-Hosted Integration Runtime
- **Monitoring & Alerts:** Azure Logic Apps
- **Version Control:** GitHub, Azure DevOps
