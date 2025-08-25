# Navigating Discrepancies and Failures with Podman on Self-Hosted GitHub Runners

Users leveraging **Podman** for build tasks on self-hosted GitHub runners may encounter a series of challenges, including inconsistencies between the GitHub web UI and the GitHub CLI (`gh`), as well as workflow failures. These issues can manifest as discrepancies in the number of visible workflow runs, conflicting status reports, and jobs that become perpetually stuck in a "queued" state.

Fortunately, a combination of understanding the underlying causes and implementing specific workarounds can mitigate these problems.

-----

## Discrepancy Between Web UI and GitHub CLI

A common point of confusion arises from the difference in workflow runs displayed in the GitHub web interface versus the output of the `gh run list` command.

  * **Web UI Shows More Runs**: The web UI provides a comprehensive view of all workflow runs, including those that are queued or stuck.

  * **API Shows Fewer Runs**: The `gh run list` command, by default, applies implicit filters that may exclude certain runs. To get a more complete picture that aligns with the web UI, you can explicitly list runs for all statuses.

    For example, you can iterate through the possible statuses to see everything:

    ```bash
    for status in completed in_progress queued requested waiting action_required cancelled failure neutral skipped stale startup_failure success timed_out; do
      gh run list --status $status
    done
    ```

-----

## Conflicting Workflow Statuses

Another perplexing issue is the conflict in status reporting between the API and the web UI. A workflow might be reported as "**cancelled**" by the `gh` command while the web UI continues to show it as "**queued**."

This is often a symptom of a known inconsistency within GitHub Actions, particularly with self-hosted runners. It can occur when the runner service loses communication with the GitHub servers. While there is no definitive user-side fix for this discrepancy, the following steps can help:

  * **Trust the Web UI**: In cases of conflict, the web UI generally reflects the most accurate current state of the workflow.
  * **Manual Intervention**: If a run is genuinely stuck, you may need to manually cancel it through the web UI.
  * **Check Runner Logs**: Investigate the logs on your self-hosted runner for any communication errors. The logs are typically located in the `_diag` subdirectory of your runner installation.

-----

## Stuck and Queued Runs

Workflows, particularly those targeting self-hosted runners, can become stuck in a "**queued**" state for extended periods, especially if the runner is offline.

  * **Runner Availability**: The most common reason for a perpetually queued job is that the designated self-hosted runner is not available. Ensure your runner is online, properly configured, and has the correct labels to match your workflow's `runs-on` directive. You can check the status of your runners in your repository or organization's settings under **Actions** \> **Runners**.
  * **Job Dependencies**: If your workflow has jobs that depend on others, a failure or stall in an upstream job will cause downstream jobs to remain queued.
  * **GitHub Service Status**: Occasionally, issues with GitHub's services can lead to jobs being stuck. Check the official [**GitHub Status page**](https://www.githubstatus.com/) for any ongoing incidents.

-----

## Best Practices for Running Podman on Self-Hosted Runners

To minimize the chances of encountering these issues when using **Podman** for your build tasks, consider the following best practices:

  * **Ensure Proper Permissions**: Running **Podman** in a rootless configuration is the recommended approach for security. Ensure the user running the self-hosted runner has the necessary permissions to execute **Podman** commands and manage container storage. This may involve configuring user namespaces and ensuring appropriate ownership of directories used by **Podman**.
  * **Stable Runner Environment**: Maintain a stable and reliable environment for your self-hosted runners. This includes ensuring consistent network connectivity to GitHub and sufficient system resources (CPU, memory, and disk space) to handle your build jobs.
  * **Regular Updates**: Keep both your self-hosted runner application and the **Podman** package updated to their latest versions. Updates often include bug fixes that can resolve underlying issues.
  * **Health Checks and Monitoring**: Implement monitoring for your self-hosted runners to be alerted if they go offline or become unresponsive. This can be as simple as a cron job that checks the runner service's status and sends a notification.
  * **Graceful Shutdown**: When you need to take a runner offline for maintenance, allow any in-progress jobs to complete before stopping the runner service to avoid abrupt cancellations that can lead to inconsistent states.