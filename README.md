# Metabase Serialization with GitHub Actions

This project demonstrates how to automate the export and import of Metabase configurations using GitHub Actions and Metabase’s built-in serialization features. It enables teams to manage dashboards, questions, and models as version-controlled code — streamlining deployment workflows across staging and production environments.

By leveraging GitHub Actions and Metabase's serialization API, this project allows you to:

- Automatically export the current Metabase configuration from a staging instance
- Store serialized files in your GitHub repository
- Automatically apply those changes to a production Metabase instance

This approach helps teams:

- Maintain a single source of truth for analytics configuration
- Eliminate manual re-creation of dashboards and questions between environments
- Version changes to BI assets alongside application code

> **Built for Metabase admins and data teams who want CI/CD for dashboards**  
>  
> **Note:** This project serves as a template and reference implementation. It’s designed to demonstrate key concepts and workflows, not as a turnkey production solution.  
> For more guidance on using Metabase’s serialization in practice, see the official documentation:  
> [Metabase Git-Based Workflow →](https://www.metabase.com/learn/administration/git-based-workflow)

---

## Table of Contents

- [Technologies Used](#technologies-used)
- [Workflows](#workflows)
- [Tagging](#tagging)
- [Configuration](#configuration)
  - [Secrets Configuration](#secrets-configuration)
  - [Example Configuration](#example-configuration)
- [Room for Improvement](#room-for-improvement)

---

## Technologies Used

- [Metabase](https://www.metabase.com/)
- [Metabase Serialization](https://www.metabase.com/docs/latest/installation-and-operation/serialization)
- [GitHub Actions](https://github.com/features/actions)
- [PostgreSQL](https://www.postgresql.org/)
- [ngrok](https://ngrok.com/)

---

## Workflows

This repo contains two export workflows, depending on how you plan to maintain your serialization files:

### 1. `export.yml`

This workflow performs a full export of your Metabase instance using the serialization API. It:

- Makes an API call to Metabase’s `/api/serialization/export` endpoint.
- Stores the result as a `.tgz` file.
- Commits the export artifact back into the repository (or into your preferred GitHub release or storage solution).

### 2. `export_filebased-workflow.yml`

This workflow is intended for file-based workflows where:

- The `.tgz` file is not committed directly.
- You manage individual YAML files in source control.
- On push to `main`, the YAML files are re-packaged into a `.tgz` file.
- The `.tgz` is ready for import via the Metabase serialization API.

This is useful for teams who want to treat Metabase objects as editable source files rather than opaque exports.

---

## Tagging

Each export workflow supports optional GitHub tagging to help you:

- Track which configuration was deployed at what point in time.
- Reference a specific serialized state of Metabase for rollback or migration purposes.

---

## Configuration

### Secrets Configuration

Before running the workflows, you need to set up the following secrets in your GitHub repository:

#### GitHub Repository Secrets

| Name | Description |
|------|-------------|
| `MB_DB_DBNAME` | Name of the Metabase application database |
| `MB_DB_HOST` | Host of the Metabase application database |
| `MB_DB_PORT` | Port of the Metabase application database |
| `MB_DB_USER` | Database user |
| `MB_DB_PASS` | Database password |
| `MB_PREMIUM_EMBEDDING_TOKEN` | Metabase token (if applicable) |
| `METABASE_URL` | Base URL of the Metabase instance |
| `METABASE_API_KEY` | Metabase API key |
| `PAT_TOKEN` | GitHub Personal Access Token |
| `GITHUB_TOKEN` | GitHub Actions token (default available) |

### Ngrok (Optional)

Ngrok is used to expose a local container or VM-hosted Metabase instance for testing the workflow against a private or local environment.

---

### Example Configuration

1. **Add Secrets**

Go to your GitHub repo → `Settings` → `Secrets and variables` → `Actions` → Add the secrets listed above.

2. **Set Permissions**

Ensure the following are enabled under `Settings` → `Actions` → `General`:

- Allow GitHub Actions to access secrets
- Enable `Read and write` under "Workflow permissions"

3. **Workflow Triggers**

Each workflow can be triggered by:

- A `push` to the `main` branch
- A scheduled cron job (customizable)

Feel free to modify these based on your team’s workflow.

---

## Room for Improvement

- Add retry logic for imports to avoid failures due to transient network/API errors.
- Add CI test hooks to validate YAML structure before packaging for import.
- Customize tagging and release strategy for better version control.
- Enhance Slack or email notification for success/failure.
- Expand compatibility for non-PostgreSQL environments.

