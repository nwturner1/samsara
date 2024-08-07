## Data Manipulation

### 1. Which channel sourced the most pipeline? How does this look by sales segment?
The channel that sourced the most pipeline is Outbound with a total pipeline amount of $34,957,059.92.

Pipeline sourced by different channels and sales segments:

ChannelName	| SalesSegment | PipelineAmount
--- | --- | ---
Adwords	| Commercial | $1,503,281.00
Adwords	|Enterprise	|$1,813,726.00
Adwords	|Mid Market	|$700,646.40
Event	|Commercial	|$65,997.64
Event	|Enterprise	|$420,769.70
Event	|Mid Market	|$139,035.70
Outbound|	Commercial	|$9,049,766.00
Outbound|	Enterprise	|$21,634,660.00
Outbound|	Mid Market	|$4,272,637.00
Webinar	|Commercial	|$298,348.00
Webinar	|Enterprise	|$3,419,841.00
Webinar	|Mid Market	|$74,736.31
Website	|Commercial	|$2,015,726.00
Website	|Enterprise	|$2,309,105.00
Website	|Mid Market	|$837,474.80


### 2. What information do you need to know to understand the ROI (return on investment) of each channel?
To understand the ROI of each channel, we need the following information:

* Cost associated with each marketing and sales touchpoint.
* The revenue generated from the opportunities attributed to each channel.
* The duration and frequency of touchpoints within each channel.

### 3. How did you structure your data table and why? What do you think are the important output dimensions?
The data table is structured to include the following columns:

* OpportunityId: To identify each unique opportunity.
* TouchpointId: To track the specific touchpoint.
* ChannelName: To know which channel the touchpoint belongs to.
* PipelineAmount: To quantify the pipeline attributed to the touchpoint.
* SalesSegment: To analyze the pipeline by different sales segments.
* The important output dimensions are:
    1. ChannelName
    2. SalesSegment
    3. PipelineAmount
    
    These dimensions allow us to analyze the performance of different channels and their contribution to the pipeline in different sales segments.

### 4. What kind of data validations and checks would you implement to make sure that downstream stakeholders have confidence in the insights they are generating from this?
To ensure confidence in the data:

* Validate the date formats and ranges for touchpoint and opportunity dates.
* Ensure there are no duplicate touchpoints for the same opportunity within the 90-day window.
* Check for any missing values or inconsistencies in the merged data.
* Implement checks to confirm that the pipeline amount is correctly attributed to the first touchpoint.

## Systems Design

### 1. Data Platforms and Stack
* Data Storage: AWS S3 for raw and processed data, RDS for storing structured source data, Amazon Redshift or Google BigQuery for output data.
* Data Processing: AWS Glue for ETL, AWS Lambda if the datasets are small.
* Machine Learning: Amazon SageMaker for developing attribution models (if needed).
* Data Access: Amazon QuickSight for visualization, AWS API Gateway for API access.

### 2. Identifying Risks and Vulnerabilities
Data Security and Privacy:

* Ensure data is encrypted both in transit and at rest.
* Implement IAM roles and policies to control access to data.
* Regularly audit access logs and policies.

Data Quality:

* Implement data validation checks during the ETL process.
* Monitor data quality metrics and set alerts for anomalies.

System Reliability:

* Use Airflow or AWS Step Functions to manage retries and error handling in the ETL pipeline.
* Set up monitoring and logging using Amazon CloudWatch.

### 3. Maintenance and Scaling
Monitoring and Maintenance:

* Use Amazon CloudWatch to monitor system performance and set up alerts for any issues.
* Regularly review and update ETL processes and machine learning models.
* Implement automated testing for the entire pipeline.

Scaling:

* Use AWS auto-scaling features for services like Lambda and Glue. Run multiple Glue jobs in parallel to apply multiple attribution models, orchestrating the pipeline with Airflow.
* Ensure the database can handle increased load by using Amazon Aurora with auto-scaling.
* Optimize data storage and retrieval by partitioning data in S3 and using efficient database indexing.

Continuous Improvement:

* Continuously gather feedback from stakeholders and refine the system.
* Implement A/B testing for different attribution models and refine them based on performance.