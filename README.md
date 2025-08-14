# Cortex AISQL Powered Call Center Analytics

## Overview

Learn how to build a comprehensive call center analytics solution leveraging Snowflake's Cortex AISQL for intelligent audio transcription (Cortex AI Transcribe), conversation analysis, and speaker identification. The solution integrates Streamlit dashboards to provide organizations with actionable insights from call center conversations through advanced AI-powered analytics, sentiment analysis, and natural language querying capabilities on audio file.

You'll learn to architect an end-to-end analytics pipeline that seamlessly processes audio files, extracts meaningful conversation insights, and delivers an intuitive conversational interface enabling business users to query call center data using natural language—all powered by Snowflake's integrated Cortex AISQL platform.


## Prerequisites
- A Snowflake Account
- 5 Minutes time  

Here you can get a free [Snowflake Trial Account](https://signup.snowflake.com/).

## Setup
All you need to do is to execute the following SQL statements in your Snowflake Account.  

```sql

USE ROLE ACCOUNTADMIN;

-- Create a warehouse
CREATE WAREHOUSE IF NOT EXISTS AI_WH WITH WAREHOUSE_SIZE='X-SMALL';

-- Create a fresh Database
CREATE OR REPLACE DATABASE CALL_CENTER_DEMO_DB;

-- Create the API integration with Github
CREATE OR REPLACE API INTEGRATION GITHUB_INTEGRATION_CALL_CENTER_DEMO
    api_provider = git_https_api
    api_allowed_prefixes = ('https://github.com/michaelgorkow/')
    enabled = true
    comment='Git integration with Michael Gorkows Github Repository.';

-- Create the integration with the Github demo repository
CREATE GIT REPOSITORY GITHUB_REPO_CALL_CENTER_DEMO
	ORIGIN = 'https://github.com/michaelgorkow/snowflake-call-center-analytics' 
	API_INTEGRATION = 'GITHUB_INTEGRATION_CALL_CENTER_DEMO' 
	COMMENT = 'Github Repository from Michael Gorkow with a demo for Call Center Analytics.';

-- Run the installation script
EXECUTE IMMEDIATE FROM @CALL_CENTER_DEMO_DB.PUBLIC.GITHUB_REPO_CALL_CENTER_DEMO/branches/main/setup.sql;
```


