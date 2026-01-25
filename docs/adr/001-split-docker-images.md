# 1. Split Frontend and Backend Container Images

Date: 2025-01-26

## Status

Accepted

## Context

The project originally utilized a single Dockerfile or a coupled build process for both the frontend (Next.js) and backend (Python/FastAPI) components. As the application grows, managing dependencies, build times, and deployment lifecycles for two distinct technology stacks within a single context becomes inefficient. Scaling them independently was also difficult.

## Decision

We have decided to split the containerization strategy into two separate Dockerfiles:
*   `Dockerfile.api`: For the Python backend.
*   `Dockerfile.frontend`: For the Next.js frontend.

## Consequences

### Positive
*   **Independent Scaling**: The frontend and backend services can now be scaled independently based on their specific resource usage (e.g., CPU vs Memory).
*   **Optimized Builds**: Changes to frontend code will not invalidate the backend build cache, and vice-versa, leading to faster CI/CD pipelines.
*   **Separation of Concerns**: Each Dockerfile focuses solely on the requirements of its specific service, making them cleaner and easier to maintain.

### Negative
*   **Operational Complexity**: Deployment now requires managing two separate container images and services instead of one.
*   **Configuration**: Orchestration (like Docker Compose or Kubernetes) needs to explicitly handle networking between the two containers.
