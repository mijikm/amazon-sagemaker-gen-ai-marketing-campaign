# amazon-sagemaker-gen-ai-marketing-campaign

### Project 
GenAI-Powered Marketing Campaign Built with Amazon SageMaker

### Business Use Case
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
  - Enter project details >
    - Project name: `project_analytics`
    - Project profile: `All capabilities` (analyse data and build ML and GenAI models/apps powered by Amazon Bedrock, Amazon EMR, AWS Glue, Amazon Athena, Amazon SageMaker AI and Amazon SageMaker Lakehouse)
  - Click `Continue`
  - Scroll down and replace the defaults of glueDbName and redshiftDbName with the project_analytics and then click Continue.
    - Lakehouse Database (name of the glue database): `project_analytics`
      - *This will create a database in Amazon SageMaker Lakehouse for storing tables in S3 and Amazon Athena resources for SQL workloads.
    - RedshiftServerless : `project_analytics`
    - *This will create an Amazon Redshift Serverless workgroup for SQL workloads.
  - Click `Continue`
