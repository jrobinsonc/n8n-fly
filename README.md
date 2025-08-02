# Self-host n8n on Fly.io

<https://github.com/jrobinsonc/n8n-fly>

This repository includes the configuration for running a self-hosted n8n instance on Fly.io.

## Getting Started

Let's update the basic configuration:

- [The app name](https://fly.io/docs/reference/configuration/#the-app-name): `app` - This will be used to create the hostname that Fly.io will assign to your app, so ensure it's unique. It must be lowercase and can include letters, numbers, and hyphens. However, it cannot start or end with a hyphen and must be a maximum of 30 characters.
- And, these two environment variables:
  - `N8N_HOST` - This must be defined so n8n knows which hostname it’s running on, like `my-app-name.fly.dev`.
  - `WEBHOOK_URL`: This is the URL that external services use to send data back to your n8n instance.

🎉 At this point, you should be ready to [launch n8n](https://fly.io/docs/getting-started/launch/) successfully. However, before you deploy, consider reading the additional configuration below.

### Additional configuration

You might need to adjust these settings according to your needs:

- [The primary region](https://fly.io/docs/reference/configuration/#primary-region): `primary_region` - This is the region where your app's volumes and machines will be created. Keep in mind that the price varies slightly depending on the region you choose. So, if you're just playing with n8n, you can leave the region that is defined, as I believe it's the cheapest one. [Check here for pricing info](https://fly.io/docs/about/pricing/#started-fly-machines).

I also want to explain the other environment variables defined in the `env` table:

- `TINI_SUBREAPER`: This tells the tini init system to manage orphaned child processes and ensure they are properly terminated, preventing them from becoming zombie processes that can waste system resources.
- `GENERIC_TIMEZONE` and `TZ`: This is the timezone your instance will use for scheduling nodes, executing workflows, and more. I set it to `UTC` based on my personal preference, but I recommend setting your timezone to avoid confusion if you're not used to having your remote environments in UTC.
- `N8N_DIAGNOSTICS_ENABLED`: This disables the [telemetry](https://docs.n8n.io/privacy-security/privacy/) sent from your instance.
- `N8N_HIRING_BANNER_ENABLED`: This determines whether to display the n8n hiring banner in the console. Just a little cleanup.

### Considerations

The resources defined here are the **minimum required** to run n8n properly. Use these settings as a starting point. Depending on your workload and usage patterns, you may need to change them.

- CPU: 1 shared CPU
- Memory: 512MB
- Database: SQLite

This configuration also includes:

- Automatic HTTPS enforcement
- Auto-start/stop machines for cost optimization
- Minimum 1 machine always running
- Persistent data storage

## Feedback and Corrections

If you find any information in this readme that is incorrect, outdated, or unclear, or if you have suggestions for improvements, please let me know by [creating an issue](https://github.com/jrobinsonc/n8n-fly/issues/new).

Your feedback is valuable and helps ensure this doc remains accurate and helpful for everyone.
