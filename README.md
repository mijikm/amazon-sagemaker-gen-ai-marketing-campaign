# amazon-sagemaker-gen-ai-marketing-campaign

### Project 
GenAI-Powered Marketing Campaign Built with Amazon SageMaker

### Business Use Case at a High Level
Marketing Personalisation

### Project Goal
Build the end-to-end process from initial data analysis to deploying a GenAI-powered targeted marketing campaign using Amazon SageMaker (NextGen)

### AWS Services
- Amazon SageMaker (NextGen)

### Prerequisites
1. Disabling Multi-Factor Authentication (MFA)
  - Open AWS console > Go to IAM Identity Center by typing `IDC` in the console search bar
    > Go to settings > Authentication > Multi-factor authentication Configure > Disable "Prompt users for MFA" > Save changes
    - Multi-Factor Authentication (MFA) was disabled to simplify the lab environment. 
2. Setting Up Amazon SageMaker Unified Studio
  - Open AWS console > Go to Amazon Sagemaker by typing `SageMaker` in the console search bar
    > Click on the `Create a Unified Studio domain` button
  - In the SageMaker Unified Studio page,
    > `Quick setup` by default
    > Click on `Grant model access` > This will open the Amazon Bedrock page
  - In the Amazon Bedrock page,
    > Click on `Enable specific models`
    > Select the following Amazon models that will be used later in the lab : `Nova Pro` (Text & Vision), `Nova Lite` (Text & Vision), `Nova Micro` (Text), `Nova Canvas` (Image)
    > Click on the `Submit` button.
    > Close the Amazon Bedrock page and then go back to the SageMaker Unified Studio page.
- In the SageMaker Unified Studio page,
    > Expand the Quick setup settings section.
    > Domain resources name: Leave the domain name as the default. (e.g. domain-07-02-2025-222942)
    > Amazon S3 bucket for projects: Amazon SageMaker Unified Studio requires an S3 bucket for projects in your AWS account. It will use the default S3 bucket listed in the page or create a new bucket if the default does not exist.
    > In the `Bedrock model access` section at the bottom, click the refresh button. Once refreshed, you should see something like `4 approved models`. Then click on the `Continue` button.
    > Create IAM Identity Center user: Enter an email address you have access to (can be either your business or personal email). You will then receive an invitation email with a hyperlink to accept the invitation. Finally, click on the `Create domain` button.
  - Go to your email and open the invitation message. Click the Accept invitation link.
  - Sign up using your email address as your username and set a new password.
- In the AWS access portal,
  - Log in using your newly set up username and password.
  - Click the `Amazon SageMaker` tile to continue to Amazon SageMaker Unified Studio.

3. Creating Projects for the Teams
  - In the Amazon SageMaker Unified Studio,
    - Click on the `Sign in with SSO` (Single Sign-On) button > You will see the SageMaker Studio landing page. Here you can create new projects and view projects that you have been added to. Projects enable a group of users to collaborate on various business use cases by performing data analysis, organise workflows, develop machine learning models, build generative AI apps, and more.

3.1 Create Analytics Team Project
- Click on the `Create project` button
- Enter project details
  - Project name: `project_analytics`
  - Project profile: `All capabilities` (analyse data and build ML and GenAI models/apps powered by Amazon Bedrock, Amazon EMR, AWS Glue, Amazon Athena, Amazon SageMaker AI and Amazon SageMaker Lakehouse)
- Click `Continue`
- Scroll down and replace the defaults of glueDbName and redshiftDbName with the project_analytics and then click Continue.
  - Lakehouse Database (name of the glue database): `project_analytics`
    - *This will create a database in Amazon SageMaker Lakehouse for storing tables in S3 and Amazon Athena resources for SQL workloads.
  - RedshiftServerless : `project_analytics`
    - *This will create an Amazon Redshift Serverless workgroup for SQL workloads.
- Click `Continue` > Click `Create project`

3.2 Create ML and GenAI Team Project
- Click on project_analytics in the top bar, then on the Create project button.
- Enter project details
  - Project name: `project_ml`
  - Project profile: `All capabilities`
- Click `Continue`
- Scroll down and replace the defaults of glueDbName and redshiftDbName with the project_ml and then click Continue.
  - Lakehouse Database (name of the glue database): `project_ml`
    - *This will create a database in Amazon SageMaker Lakehouse for storing tables in S3 and Amazon Athena resources for SQL workloads.
  - RedshiftServerless : `project_ml`
    - *This will create an Amazon Redshift Serverless workgroup for SQL workloads.
- Click `Continue` > Click `Create project`
- Click on View projects to see the 2 projects.

### Business Use Case
- Situation: AnyCompany Food & Beverage, a 25-year-old manufacturer, faces an unprecedented sales decline and a 30% marketing budget cut in 2025, while new digital-first competitors have reduced their market share from 28% to 22% through lower pricing and data-driven strategies.
- Task: the CEO tasks Sarah's newly formed specialized team to develop and implement a sophisticated, targeted marketing campaign as part of a broader digital transformation initiative.
- Action: Sarah assembles a cross-functional team with Samantha (Data Analyst/Engineer) and Javier (Data Scientist) to leverage data-driven insights and Generative AI for identifying and targeting high-potential products.
- Result (Expected): the team aims to reverse the sales decline and achieve a 10 percentage point increase in market share (from 22% to 32%) by Q4 2025 through rapid deployment of data-driven marketing campaigns, despite operating with reduced budget constraints.

### Implementation
##### 1) Understand sales trends and creating a new data asset
Part 1.1: Data Discovery
- Discover existing tables that could be useful for the use case
- Analyze the data to identify product sales patterns and trends
Part 1.2: ETL Pipeline Development
- Create a notebook-based ETL workflow
- Extract and transform data from different sources
Part 1.3: Data Product Publication
- Enrich new tables with GenAI-generated business context
- Combine and publish tables as a comprehensive data product
- Publish a data product

Amazon SageMaker: Through natural conversations with Amazon Q Developer, you can gain deeper insights into your data, generate SQL queries, author code, integrate datasets, and resolve issues efficiently. 

By completing this lab, you will:
- Master SageMaker Project workspace navigation
- Develop production-grade ETL pipelines using notebooks
- Learn how to create data products
  
##### 1.1) Understand sales trends and growth rates => Data Analysis
Step 1 - Discovering my organization’s datasets
- Amazon Q will help you identify the foundational datasets you need to combine to create a new dataset that's ready for use by the ML team.

- Go to `project_analytics` project > You land in the `Project overview` page
  - Open Amazon Q by clicking on the top right icon.
  - On the Amazon Q chat section click on Continue on the info message.
  - Ask Amazon Q about where to find your data by entering the following question text into the chat box on the bottom right and clicking the Submit button.
    - Prompt: Where can I find data about my sales?
    - You'll see that Q has located our sales data table (AWS Glue tables - Lakehouse). Open it by clicking on the `Retail Sales Performance Insights` link provided by Q
    - We can see the table **sales_data** is located inside the database **customer_insights_db**.
      
Step 2 - Understanding and trusting your data
- Dive into the Data Quality tab to assess whether the dataset is reliable. **=> Data Quality tab was not available/visible in the lab**
- This tab will help you determine if proper data quality controls are in place, or if the dataset lacks the necessary mechanisms to ensure its accuracy.

Step 3 - Uncovering negative trends in my company sales performance
- Now that you're familiar with the available datasets, it’s time to dig deeper into the company’s sales performance. The key question here is: What are the negative trends affecting sales?
- Let's go to the `Query Editor` from the `Build` menu item at the top of the screen.
- From there let's have a look into the Sales data:
  - Expand the **AwsDataCatalog** catalog
  - Expand the **customer_insights_db** database
  - Click the 3 dots icon next to the **sales_data** table
  - Click **Query with Athena**. This should show us 10 lines.

Step 4 - Tackling advanced questions with the help of Amazon Q
- By asking Amazon Q insightful questions, you can quickly identify patterns or areas where sales are underperforming. Whether it’s a drop in specific product categories, regions, or time periods, Amazon Q will help you uncover those trends and provide the insights you need to take action.
- Click on the Amazon Q icon on the top right, copy-paste the following question into the chat box on the bottom right and click the Submit button.
  - Prompt: What is the worst performing region, in terms of profit, in 2024?
- Then click on the Add to querybook icon right after the Amazon Q response. Finally click the Run cell icon in the querybook.
- Keep going with your analysis. Copy-paste the following question into the Amazon Q chat box and click the Submit button.
  - Prompt: Now, can you change the query to show the worst 5 countries instead?

##### 1.2) Preparing a new dataset for the ML team => Table creation for other teams consumption
Step 1 - Building an ETL job to combine Sales data with Promotions data
Now that you're familiar with the available tables, it’s time to generate a new table that you'll later share with other teams.
- Download this notebook.
- Open JupyterLab from the Build menu item at the top of the screen.
- Upload the downloaded notebook by dragging it into the JupyterLab File browser or using the upload icon.
- Double-click on the join_lakehouse_tables.ipynb notebook to open it and follow the instructions within.
Note: Run each notebook cell in sequence, carefully following the instructions. To execute a Code cell, select it and click the Run button as shown below:

In the notebook you will create a new analytical table that:
🔗 Combines sales transaction records from S3 with promotional data from Redshift (see Sagemaker Lakehouse in action)
📈 Calculates the number of active promotions per product category and region at the time of each sale
🤖 Provides a cleaned and optimized dataset ready to be shared with the Machine Learning team

##### 1.3) Publishing the new dataset as new data asset making it discoverable
