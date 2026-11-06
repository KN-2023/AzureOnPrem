# End-to-End Azure Data Engineering Pipeline
### Project Architecture

<img width="400" height="200" alt="Corrected Medallion Architecture Diagram" src="https://github.com/user-attachments/assets/65aaae9b-d4b9-4c81-a8bf-67f6ea104dc6" />

- End-to-end data pipeline built with Azure Data Factory and ADLS Gen2.
- Ingests on-premises CSV, REST API, and Azure SQL data.
- Implements Bronze, Silver, and Gold layers for data processing.
- Uses Mapping Data Flows and watermark-based incremental loading.
- Automates orchestration and failure alerts using ADF and Logic Apps.
- Uses GitHub and Azure DevOps for version control.

### Technology Stack

- **Data Integration:** Azure Data Factory
- **Data Storage:** Azure Data Lake Storage Gen2, Azure SQL Database
- **Data Processing:** ADF Mapping Data Flows
- **Connectivity:** Self-Hosted Integration Runtime
- **Monitoring & Alerts:** Azure Logic Apps
- **Version Control:** GitHub, Azure DevOps

### Data Sources

- **On-Premises:** CSV files containing passenger, airline, and flight data.
- **REST API:** JSON data ingested through API integration.
- **Azure SQL Database:** Booking data extracted using watermark-based incremental loading.

### Pipeline Overview

The parent pipeline orchestrates the execution of the following child pipelines:

<img width="900" height="90" alt="pipeline_clear" src="https://github.com/user-attachments/assets/438269ea-1df0-458f-968a-e1ef2999c68a" />

- **On-Premises Ingestion:** Loads CSV files into Azure Data Lake Storage.
- **API Ingestion:** Retrieves JSON data from a REST API.
- **SQL Ingestion:** Performs watermark-based incremental data loading from Azure SQL Database.

### On-Premises Data Ingestion
<table>
<tr>
<td valign="top" width="200">
<img src="https://github.com/user-attachments/assets/96482b9a-01ed-4941-8c14-dfb6b8c03e65" width="200" height = "200" alt="ForEach activity">
</td>
<td valign="top">
<ul>
<li>Uses Self-Hosted Integration Runtime (SHIR) to connect to on-premises files.</li>
<li>Uses parameterized datasets and a ForEach activity to dynamically ingest multiple CSV files into ADLS Gen2.</li>
</ul>
</td>
</tr>
</table>

### API Data Ingestion
<img width="400" height="90" alt="webapi_copy_clear" src="https://github.com/user-attachments/assets/f96ec18d-1d82-40f3-94c5-144647644e38" />

- Uses ADF Web and Copy activities to retrieve JSON data from a REST API and store it in ADLS Gen2.

## Watermark-based Incremental Data Loading

**Before Pipeline Execution:**

<img width="350" height = "150" alt="lastload_json_before" src="https://github.com/user-attachments/assets/6554045f-72a0-4859-83d0-e7089478eb7a" />

**Pipeline:**

<img width="500" alt="incremental_pipeline" src="https://github.com/user-attachments/assets/eb09e403-723c-4ea1-9201-3bfcf2ee1522" />

**After Pipeline Execution:**

<img width="350" height = "150" alt="lastload_json_after" src="https://github.com/user-attachments/assets/57836889-9696-4e97-9df0-f4cda450fe85" />

- Implements watermark-based loading using LastLoad and LatestLoad lookup activities.
- Copies only new records from Azure SQL Database to ADLS Gen2.
- Updates the watermark after successful execution.
  
### Silver Layer
<img width="1000" height="350" alt="dataflow_clear" src="https://github.com/user-attachments/assets/6f3b64d9-8396-47f7-9149-842cfb189362" />

- Uses ADF Mapping Data Flows to clean, validate, and transform ingested data before storing it in the Silver layer.
### Gold Layer
<img width="4048" height="844" alt="gold_dataflow_clear" src="https://github.com/user-attachments/assets/6a32a628-de3c-43b3-b8d0-5304cb110112" />
- Uses ADF Mapping Data Flows to join, aggregate, and rank data, creating business-ready datasets for analytics.

### Error Handling & Notifications
<img width="400" height="200" alt="logicapp_email_clear" src="https://github.com/user-attachments/assets/4ff47a4c-a14d-4938-a772-844269975ebb" />
<img width="425" height="200" alt="logicapp_trigger_clear" src="https://github.com/user-attachments/assets/caa519a7-8f8b-469b-9c86-874b1b30169b" />

- Integrates Azure Logic Apps with ADF to send automated notifications containing pipeline execution status and error details.

### Execution Results
<img width="600" height="150" alt="gold_businessview_clear" src="https://github.com/user-attachments/assets/1739df11-147a-4848-870c-d1b94467d2e8" />

- Successfully executed ingestion and transformation pipelines, validating the end-to-end data flow across the Bronze, Silver, and Gold layers.
