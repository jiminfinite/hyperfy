# Hyperfy ⚡️

## Overview

<div align="center">
  <img src="overview.png" alt="Hyperfy Ecosystem" width="100%" />
</div>

## 🧬 Features

- Standalone persistent world
- Host them on your own domain
- Connect via Hyperfy for portable avatars
- Realtime content creation in-world
- Realtime coding in-world (for devs)
- Fully interactive and interoperable app format
- Highly extensible

## 🦹‍♀️ Use Cases

- Live events
- Storefronts
- Podcasts
- Gaming
- Social

## 🚀 Quick Start

### Prerequisites

- Node 22.11.0+ (eg via nvm)

### Install

```bash
git clone https://github.com/hyperfy-xyz/hyperfy.git my-world
cd my-world
cp .env.example .env
npm install
npm run dev
```

## 🌱 Alpha

This project is still in alpha as we transition all of our [reference platform](https://github.com/hyperfy-xyz/hyperfy-ref) code into fully self hostable worlds.
Most features are already here in this repo but still need to be connected up to work with self hosting in mind.
Note that APIs are highly likely to change during this time.

# The Cafe - Hyperfy Admin Integration

This repository contains the code for integrating The Cafe's backend with a Hyperfy world, including admin privilege management.

## Overview

This integration allows users from The Cafe website to seamlessly enter the Hyperfy world with their account information, including admin privileges if they have them.

## How It Works

1. When a user clicks to enter the Hyperfy world from The Cafe website, they are redirected to the Hyperfy world URL with a session token.
2. The Hyperfy world verifies this session token with The Cafe's backend API.
3. If the user has admin privileges in the database, they are granted admin privileges in the Hyperfy world.
4. Admin users get access to special features and controls in the Hyperfy world.

## Setup Instructions

### 1. Environment Variables

Set up the following environment variables in your Hyperfy world:

- `API_URL`: The URL of your backend API (e.g., `https://api.thecafe.com`)
- `ALCHEMY_API_KEY`: Your Alchemy API key for blockchain interactions

### 2. Backend API

Implement the `/api/verify-session` endpoint in your backend as specified in `backend-api-spec.md`.

### 3. Frontend Integration

Add the following code to your frontend to redirect users to Hyperfy with a session token:

```javascript
function redirectToHyperfy(user) {
  // Generate a session token
  const sessionToken = generateSecureToken();
  
  // Save the session token in your database
  saveSessionToken(user.walletAddress, sessionToken);
  
  // Redirect to Hyperfy with the session token
  const hyperfyUrl = `https://hyperfy.io/your-world?session=${sessionToken}`;
  window.location.href = hyperfyUrl;
}
```

## Testing Admin Privileges

1. Log in to The Cafe website with an admin account.
2. Click the link to enter the Hyperfy world.
3. Once in the Hyperfy world, type `/checkadmin` in the chat to verify your admin status.
4. Admin users should see an admin control panel in the top-right corner of the screen.

## Security Considerations

- Session tokens should be short-lived (expire after a few minutes).
- Always verify that the wallet address matches the session token.
- Use HTTPS for all API calls.
- Implement rate limiting to prevent brute force attacks.

## Troubleshooting

- If admin privileges are not being granted, check the console logs for error messages.
- Verify that the session token is being correctly passed in the URL.
- Ensure that the backend API is correctly verifying the session token.
- Check that the user has the `hyperfyAdmin` flag set to `true` in the database.

