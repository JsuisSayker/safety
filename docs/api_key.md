# API keys for Safety CLI

Safety API keys are useful when you want to authenticate scans in a non-interactive environment such as CI/CD, Docker builds, or production automation. They also let you provide a consistent credential when you are not using a browser-based `safety auth login` flow.

For day-to-day local development, `safety auth login` is usually the simplest option. For scripts, automation, or headless environments, an API key is often the better fit.

## When to use an API key

Use an API key when you want to:

- run scans in GitHub Actions, GitLab CI, Azure Pipelines, or other automation
- scan in a container or remote machine without a browser session
- set a production or staging scan stage explicitly with `--stage`
- inject the credential from a secret manager or environment variable

## API Key

This is a step by step guide on how to get an API key that can be used for safety. Using an API Key
with safety gives you access to the latest vulnerabilities. The freely available database
is synced only once per month.

In order to get an API Key you need a subscription on [safetycli.com](https://safetycli.com).

## Step 1 - Sign Up

Go to [safetycli.com](https://safetycli.com) and click on `sign up`.

## Step 2 - Start your free trial

Choose the plan best suited to your team's need and start your 14-day free trial.

## Step 3 - Go back to account page

Once payment is complete, you'll be redirected to your account page.

## Step 4 - Copy your API key

Copy your API Key from your account homepage and store it in a secure secret manager or environment variable.

Example:

```bash
export SAFETY_API_KEY="your-api-key"
```

You can then use it directly:

```bash
safety --key "$SAFETY_API_KEY" scan --output json
```

Or with an environment variable and a project scan:

```bash
SAFETY_API_KEY="your-api-key" safety scan --stage production
```

## Step 5 - Verify the configuration

Check the CLI status to confirm authentication is available:

```bash
safety auth status
```

If you are running a local interactive session, you may prefer the browser-based flow instead:

```bash
safety auth login
```

For remote terminals or headless systems:

```bash
safety auth login --headless
```

## Best practices

- store the key in a secret manager instead of committing it to source control
- rotate keys periodically if your team uses shared credentials
- prefer `SAFETY_API_KEY` in CI pipelines so the secret stays out of command history and logs
- use local browser login for developer machines and API keys for automated workflows
