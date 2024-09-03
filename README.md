# uptime-kuma-create-maintenance
Action to create an uptime kuma maintenace and add a monitor
## Action.yml

This repository contains an action to create an uptime kuma maintenance and add a monitor. The action is designed to be used in workflows to automate the process of managing maintenance and monitoring in uptime kuma.

### Usage

To use this action, include the following step in your workflow:

```yaml
- name: Create Uptime Kuma Maintenance
    uses: actions/uptime-kuma-create-maintenance@v1
    with:
        UPTIME_USERNAME: "${{ vars.UPTIME_USERNAME }}"
        UPTIME_PASSWORD: "${{ secrets.UPTIME_PASSWORD }}"
        UPTIME_API_URL: "${{ vars.UPTIME_API_URL }}"
        MAINTENANCE_TITLE: "Service Deployment"
        MONITOR_ID: "${{ vars.UPTIME_MONITOR_ID }}"
        MONITOR_NAME: "Service Maintenance"
```

Make sure to replace the placeholders with the appropriate values. The `api-key` and `monitor-id` should be stored as secrets in your repository.

### Inputs

- `UPTIME_USERNAME` (required): The username for accessing the uptime kuma API.
- `UPTIME_PASSWORD` (required): The password for accessing the uptime kuma API.
- `UPTIME_API_URL` (required): The URL of the uptime kuma API.
- `MAINTENANCE_TITLE` (required): The title of the maintenance.
- `MONITOR_ID` (required): The ID of the monitor to add to the maintenance.
- `MONITOR_NAME` (required): The name of the monitor.

### Outputs

This action outputs the maintenance ID. This can be used in later actions to manupilate the maintenace.
```
outputs:
  maintenance_id:
    description: 'The generated maintenance ID'
    value: ${{ steps.create-maintenance.outputs.maintenance_id }}
```

### Example

Here's an example of how to use this action in a workflow:

```yaml
name: Uptime Kuma Maintenance

on:
    schedule:
        - cron: '0 0 * * *'

jobs:
    create-maintenance:
        runs-on: ubuntu-latest

        steps:
            - name: Checkout repository
                uses: actions/checkout@v2

            - name: Create Uptime Kuma Maintenance
                uses: actions/uptime-kuma-create-maintenance@v1.0.0
                with:
                    UPTIME_USERNAME: "${{ vars.UPTIME_USERNAME }}"
                    UPTIME_PASSWORD: "${{ secrets.UPTIME_PASSWORD }}"
                    UPTIME_API_URL: "${{ vars.UPTIME_API_URL }}"
                    MAINTENANCE_TITLE: "Service Deployment"
                    MONITOR_ID: "${{ vars.UPTIME_MONITOR_ID }}"
                    MONITOR_NAME: "Service Maintenance"
```

This workflow will create a maintenance in uptime kuma every day at midnight.
