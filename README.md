# Metabase Serialization for Import and Export

This repository provides a setup for importing and exporting Metabase data models using serialization. The workflow automates the process of exporting data models from a staging Metabase instance and importing them into a production instance. This is just a base line and should be considered a template to reference along with help articles such as the following.
https://www.metabase.com/learn/administration/git-based-workflow

## Table of Contents
* [Technologies Used](#technologies-used)
* [Configuration](#configuration)
* [Workflows](#workflows)
  * [Export Data Model](#export-data-model)
  * [Import Data Model](#import-data-model)
* [Room for Improvement](#room-for-improvement)

## Technologies Used
- [Metabase](https://www.metabase.com/)
- [Metabase Serialization](https://www.metabase.com/docs/latest/installation-and-operation/serialization)
- [GitHub Actions](https://github.com/features/actions)
- [PostgreSQL](https://www.postgresql.org/)
- [ngrok](https://ngrok.com/)


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

