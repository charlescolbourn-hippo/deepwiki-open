# 2. Adoption of Knative Service (Cloud Run) for Deployment

Date: 2025-01-26

## Status

Accepted

## Context

To support a scalable, production-ready deployment on Google Cloud Platform, we needed a declarative way to define our infrastructure and service requirements. The previous deployment method was less formalized for cloud environments.

## Decision

We have adopted the Knative Service definition format (`service.yaml`) tailored for Google Cloud Run. This configuration defines the deployment for both the frontend and backend services within a single logical unit or coordinated set of services.

Key configurations included:
*   `autoscaling.knative.dev/maxScale: '100'` for handling load.
*   Environment variable injection for secrets (API Keys) and configuration.
*   GCS Fuse volume mounts for persistent storage (`deepwiki-data`).

### Deployment Workflow

For consistent deployments, the following workflow is used:
1.  **Container Build**: Images are built remotely using Google Cloud Build to ensure environment consistency (e.g., using `cloudbuild.frontend.yaml` for the frontend).
    ```bash
    gcloud builds submit --config cloudbuild.frontend.yaml .
    ```
2.  **Service Update**: The Cloud Run service is updated using the declarative `service.yaml` file.
    ```bash
    gcloud run services replace service.yaml --region europe-west2
    ```

## Consequences

### Positive
*   **Serverless Operations**: Cloud Run manages the infrastructure, patching, and scaling automatically.
*   **Declarative Infrastructure**: The `service.yaml` serves as a single source of truth for the deployment configuration.
*   **Cost Efficiency**: Scale-to-zero capabilities (if configured) and paying only for compute used.

### Negative
*   **Platform Lock-in**: The specific annotations (`run.googleapis.com`) are specific to Google Cloud Run, making migration to generic Knative or other platforms slightly more involved.
*   **Cold Starts**: Serverless workloads may experience cold starts if not kept warm (though `minScale` can mitigate this).
