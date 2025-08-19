# Deployment Guide

## GitHub Actions Setup

This project includes a GitHub Actions workflow that automatically deploys to Cloudflare Workers when you push to the `main` or `master` branch.

### Required Secrets

You need to configure the following secrets in your GitHub repository:

1. **CLOUDFLARE_API_TOKEN**: Your Cloudflare API token
2. **CLOUDFLARE_ACCOUNT_ID**: Your Cloudflare account ID

### How to Get These Values

#### 1. Cloudflare API Token

1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. Navigate to **My Profile** → **API Tokens**
3. Click **Create Token**
4. Use the **Custom token** template
5. Configure permissions:
   - **Zone Resources**: Include → All zones
   - **Account Resources**: Include → All accounts
   - **Permissions**:
     - Account: Workers Scripts:Edit
     - Zone: Workers Routes:Edit
6. Click **Continue to summary** and then **Create Token**
7. Copy the token value

#### 2. Cloudflare Account ID

1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. Look at the right sidebar - your Account ID is displayed there
3. Or go to **Workers & Pages** → **Overview** and find your Account ID

### Setting Up Secrets in GitHub

1. Go to your GitHub repository
2. Click **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret**
4. Add each secret:
   - Name: `CLOUDFLARE_API_TOKEN`
   - Value: Your API token
   - Name: `CLOUDFLARE_ACCOUNT_ID`
   - Value: Your account ID

### How It Works

The workflow will:

1. Trigger on pushes to `main`/`master` branches
2. Install dependencies
3. Build the project using `npm run build`
4. Deploy to Cloudflare using Wrangler
5. Use the official Cloudflare Wrangler Action

### Manual Deployment

If you prefer to deploy manually:

```bash
npm run deploy
```

This will build and deploy your application to Cloudflare Workers.

### Troubleshooting

- Ensure your `wrangler.jsonc` is properly configured
- Check that your Cloudflare account has Workers enabled
- Verify your API token has the correct permissions
- Check the Actions tab in GitHub for detailed logs
