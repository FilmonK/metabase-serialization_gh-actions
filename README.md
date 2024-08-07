# Metabase Serialization using Github Actions

This repository provides a setup for importing and exporting Metabase data models using serialization from a **single staging instance** to a **single production instance**. The workflow automates the process of exporting data models from a staging Metabase instance and importing them into a production instance. This example has been broken up into two workflows but there's no reason they can't be combined based on the use case.
This is just a base line and should be considered a template to reference along with help articles such as the following. 
https://www.metabase.com/learn/administration/git-based-workflow

## Table of Contents
* [Technologies Used](#technologies-used)
* [Configuration](#configuration)
* [Workflows](#workflows)
* [Room for Improvement](#room-for-improvement)

## Technologies Used
- [Metabase](https://www.metabase.com/)
- [Metabase Serialization](https://www.metabase.com/docs/latest/installation-and-operation/serialization)
- [GitHub Actions](https://github.com/features/actions)
- [PostgreSQL](https://www.postgresql.org/)
- [ngrok](https://ngrok.com/)

## Workflows
There are two export workflows.
- "export.yml" goes through the process of making an API call to serialize and create the .tgz file
- "export_filebased-workflow.yml" assumes you will be making edits locally to the YML files of an already decompressed serialization export. As those files are pushed to the main branch of your repo, they are compressed into a .tgz file that can be used to import using the serialization API.

## Tagging
Tags are applied to the export workflows

## Configuration

### Secrets Configuration

Before running the workflows, you need to set up the following secrets in your GitHub repository:

1. **GitHub Repository Secrets:**
   - `MB_DB_DBNAME`: The database name for Metabase.
   - `MB_DB_HOST`: The database host.
   - `MB_DB_PORT`: The database port.
   - `MB_DB_USER`: The database user.
   - `MB_DB_PASS`: The database password.
   - `MB_PREMIUM_EMBEDDING_TOKEN`: The Metabase embedding token.
   - `METABASE_URL`: The URL of the Metabase instance.
   - `METABASE_API_KEY`: The API key for Metabase.
   - `PAT_TOKEN`: Personal Access Token for accessing the repositories.
   - `GITHUB_TOKEN`: (If not already available) GitHub token for the workflow.
  
2. **Ngrok:**
Ngrok is included soley as a means to create a passthrough to a local device or container that isn't publically accessible.

3. **Branches and scheduling:**
The YML files are currently set to perform Actions based on when there's a push to the main branch of a repo, as well as a cron schedule. Make adjustments that are more suited to your workflow, whether that's a different schedule or branch logic.

4. **Github permissions:**
Make sure the needed permissions are set in Settings --> Actions --> General
   - Actions Permissions
   - Workflow permissions


### Example Configuration

1. **Setting Up Secrets in GitHub:**
   - Go to your GitHub repository.
   - Navigate to `Settings` > `Secrets and variables` > `Actions`.
   - Add the required secrets with their corresponding values.

2. **Environment Variables:**
   - The workflows use environment variables to reference the secrets.



## Room for Improvement
- Implement retry logic for the import process to handle transient errors.
- Enhance logging for better monitoring and troubleshooting.
- Ensure that the workflows are compatible with other database engines.
- Add more comprehensive error handling and notifications for workflow failures.

By following these configurations, you can automate the import and export processes for Metabase data models using GitHub Actions and ensure sensitive information is securely managed through GitHub Secrets.

