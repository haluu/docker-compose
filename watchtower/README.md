# Watchtower Container Updater

This directory contains the Docker Compose configuration for Watchtower, an automated Docker container update service. Watchtower monitors your running containers, checks for updated images, and automatically updates them with zero downtime, keeping your services secure and up-to-date.

## Features

- **Automatic Updates**: Monitors and updates Docker containers automatically
- **Label-Based Filtering**: Only updates containers with specific labels
- **Scheduled Updates**: Run updates on a cron schedule
- **Zero Downtime**: Gracefully stops and restarts containers
- **Cleanup**: Automatically removes old images after updates
- **Notifications**: Send update notifications via Slack or other channels
- **Monitor Mode**: Optional dry-run mode to see what would be updated
- **Selective Updates**: Control which containers to update

## File Structure

```
watchtower/
├── .env                  # Environment variables configuration
├── docker-compose.yml    # Watchtower service definition
└── README.md            # This file
```

## Update Schedule

The default schedule `0 0 2 * * MON` means:
- Updates run at 2:00 AM every Monday
- Uses cron format: `seconds minutes hours day-of-month month day-of-week`

Common schedule examples:
- `0 0 2 * * *` - Daily at 2 AM
- `0 0 2 * * MON` - Weekly on Monday at 2 AM
- `0 0 2 1 * *` - Monthly on the 1st at 2 AM
- `0 0 */6 * * *` - Every 6 hours

## Label-Based Updates

With `LABEL=true`, only containers with this label will be updated:
```yaml
labels:
  - com.centurylinklabs.watchtower.enable=true
```

This gives you fine-grained control over which containers Watchtower manages.

## How It Works

1. **Monitoring**: Watchtower connects to Docker via `/var/run/docker.sock`
2. **Checking**: At scheduled times, checks Docker Hub for newer images
3. **Updating**: If a new image is found for a labeled container:
   - Pulls the new image
   - Stops the current container gracefully
   - Starts a new container with the same configuration
4. **Cleanup**: Removes the old image (if `CLEANUP=true`)
5. **Notification**: Sends notification to Slack about the update

## Slack Notifications

To set up Slack notifications:

1. Create a Slack webhook:
   - Go to https://api.slack.com/apps
   - Create a new app or select existing
   - Enable Incoming Webhooks
   - Create a webhook URL

2. Configure in `.env`:
   ```bash
   NOTIFICATIONS=slack
   SLACK_HOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL
   SLACK_CHANNEL=#docker-updates
   ```

3. Watchtower will send notifications for:
   - Container updates
   - Update failures
   - Update summaries

## Security Considerations

- **Docker Socket Access**: Watchtower requires access to `/var/run/docker.sock` (full Docker control)
- **Label Protection**: Use `LABEL=true` to prevent unintended updates
- **Schedule Timing**: Choose update times when traffic is low
- **Monitor Mode**: Test with `WATCHTOWER_MONITOR_ONLY=true` first
- **Network Isolation**: Runs on the `proxy` network but doesn't need external access

## Notes

- Watchtower only updates containers to the same tag (e.g., `latest` to newer `latest`)
- Does not perform version upgrades (e.g., won't update `v1.0` to `v2.0`)
- Works with public and private registries
- Compatible with all containers in the Docker network
- Self-updates when labeled appropriately
