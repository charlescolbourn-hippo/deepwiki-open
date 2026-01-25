# 3. WebSocket Proxying via Next.js

Date: 2025-01-26

## Status

Accepted

## Context

The application uses WebSockets for real-time chat functionality. Direct connections from the client (browser) to the backend API can introduce Cross-Origin Resource Sharing (CORS) issues and require the client to be aware of the backend's specific URL, which adds configuration complexity across different environments.

## Decision

We have configured the Next.js frontend to act as a reverse proxy for WebSocket connections.
*   **Client Side**: The `websocketClient.ts` connects to `/ws/chat` relative to the current window location.
*   **Server Side (Next.js)**: `next.config.ts` includes a rewrite rule that forwards traffic from `/ws/chat` to the backend service defined by `TARGET_SERVER_BASE_URL`.

## Consequences

### Positive
*   **Simplified Client Config**: The client does not need to know the backend URL; it simply connects to "itself".
*   **Security**: Internal backend URLs are hidden from the public client.
*   **CORS**: Avoids complex CORS configurations on the backend for WebSocket endpoints.

### Negative
*   **Resource Usage**: The Next.js server must handle the open connections to proxy them, potentially increasing memory usage on the frontend instances.
*   **Latency**: Adds a small hop in the network path.
