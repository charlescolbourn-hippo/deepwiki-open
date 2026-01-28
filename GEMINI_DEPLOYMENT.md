# Deploying DeepWiki using Gemini CLI

This guide describes how to deploy the DeepWiki application to Google Cloud Run using the Gemini CLI agent.

## Prerequisites

1.  **Google Cloud SDK (gcloud)** installed and authenticated.
2.  **Gemini CLI** installed and configured.
3.  **Project Access:** You must have permissions to access the Google Cloud project (e.g., `deepwiki-hippowiki`) and the Artifact Registry.

## Deployment Steps

You can instruct the Gemini CLI to handle the entire deployment process. Below are the commands and prompts you can use.

### 1. Authenticate and Configure Project

First, ensure Gemini is using the correct Google Cloud identity and project context.

**Prompt for Gemini:**
> "Switch gcloud account to [YOUR_EMAIL] and set the project to deepwiki-hippowiki."

*Example:*
> "Switch gcloud account to harvinder.atwal@hippodigital.co.uk and set the project to deepwiki-hippowiki."

### 2. Build Container Images

The application consists of a frontend and a backend API, which need to be built and pushed to the Google Artifact Registry.

**Prompt for Gemini:**
> "Build the frontend and backend images using Google Cloud Build."

*Behind the scenes, Gemini will run:*
- `gcloud builds submit --config cloudbuild.frontend.yaml .`
- `gcloud builds submit --config cloudbuild.api.yaml .`

### 3. Deploy to Cloud Run

Once the images are built, you can deploy the service using the declarative `service.yaml` configuration.

**Prompt for Gemini:**
> "Deploy the service to Cloud Run using service.yaml in region europe-west2."

*Behind the scenes, Gemini will run:*
- `gcloud run services replace service.yaml --region europe-west2`

### 4. Updating Configuration (Optional)

If you need to change environment variables (like API keys) or system settings (like timeouts), ask Gemini to modify `service.yaml` before deploying.

**Example Prompts:**
- "Increase the Cloud Run timeout to 60 minutes in service.yaml."
- "Update the GOOGLE_API_KEY in service.yaml to [NEW_KEY]."

### Troubleshooting

If you encounter issues (e.g., "socket hang up" or missing diagrams), you can ask Gemini to investigate:

**Prompt for Gemini:**
> "Check the logs for the deepwiki-open service in europe-west2 and tell me why it's failing."

## One-Shot Deployment

You can also combine these steps into a single instruction if you are confident in the current state of the code.

**Prompt for Gemini:**
> "Build both the frontend and backend images using Cloud Build, and then deploy the updated service to Cloud Run in europe-west2."
