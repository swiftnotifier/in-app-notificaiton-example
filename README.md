# InApp Notification SDK

Small workspace for:

- a reusable in-app notification SDK package
- a standalone Next.js host app used to test and track notifications

## Structure

- `sdk/`
  - reusable package code
  - transport layer, React exports, shared types
- `ui/`
  - standalone Next.js host application
  - owns frontend screens and later backend/socket integration

## Current scope

- transport-driven SDK client
- optional HTTP transport implementation
- get all in-app notifications
- get customer by ID
- direct socket connection helper

## Recommended SDK usage

Create a transport in the host app, then pass it into the SDK client.

```ts
import {
  createHttpInAppNotificationTransport,
  createInAppNotificationSdkClient,
} from 'inapp-notification-sdk';

const transport = createHttpInAppNotificationTransport({
  inAppNotificationsBaseUrl: process.env.NEXT_PUBLIC_INAPP_NOTIFICATIONS_API_URL!,
  projectScopeBaseUrl: process.env.NEXT_PUBLIC_PROJECT_SCOPE_API_URL!,
  accessToken: 'token-if-needed',
});

const client = createInAppNotificationSdkClient({ transport });
```

Socket usage stays explicit:

```ts
import { createSocketConnection } from 'inapp-notification-sdk';

const socket = createSocketConnection({
  url: process.env.NEXT_PUBLIC_INAPP_SOCKET_URL!,
});
```

## Notes

- The SDK no longer depends on backend env URLs by default.
- The consuming app controls transport strategy.
- You can use direct backend calls or your own Next.js `app/api` BFF without changing the UI layer.
# in-app-notificaiton-example
