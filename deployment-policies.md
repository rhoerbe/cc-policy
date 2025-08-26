## Staging environments
- Understand the roles of each server in the staging environment.
- Collect the access methods (authentication, tools) to understand how to work in each environment. 
  Do not assume that environments are local.
- Always update images and containers after changes.
- Verify systemd service status after changes.
- Standard environments are dev, test and prod. 
- By default, test has a recent copy of prod data.
- The containers for prod and test must have completely separated environments. They must not share data or configurations.
- The staging envs are to be as consistent as possible. File, directory and env variable names shall be kept identical.
  <example>Do not name a file test.env or prod_settings.py. The staging environment must be implied only by the deployment location.</example>


## Regular deployment using containers
### Processes
- The systemd user service should handle the container lifecycle using Podman Quadlet. This implies rootless containers.
- Always pull images from GitHub Container Registry (GHCR). 
  Prod can use existing images, test must always pull the latest image.
- Verify authentication to GHCR before pulling images.
- Use the deployment scripts provided in the repository for consistency.
- Maintain rollback capability to previous versions.
- Keep the existing database instance. Do not initialize or overwrite.
### Container configuration
- Ensure proper environment separation (test vs production).
  All volumes, ports and configurations must be distinct.
  Exception: A/B and blue/green deployments may share the same database.
- Use environment variables for configuration, avoid hardcoding values.
- Securely manage sensitive information (e.g., use .env files with proper permissions).
- Implement health checks to monitor container and application status.
- Containers must be run rootless (in user space), unless privileged operation is required.
  For user-space containers lingering must be enabled.
- With defined exceptions, containers may run as root (e.g., github-runner).
- Map volumes to host directories, do not use named or anonymous volumes.
- Containers should put all logs in a single VOLUME. Typically, this is /app/log/<service> or /var/log/<service>.
### Separation of concerns
- Log rotation is handled by the host system, not the container.
- Backup is handled by the host system, not the container.

## Deployment Report
The title "Deployment Complete" requires to have successfully completed following steps
- The deployment steps have been logged into logs/deployment_<YYMMDD_HHMM>.log 
- The healthcheck status is reported by systemd as expected
- All non-destructive unit tests pass
- All read-only database verification tests pass
- The service is accessible (e.g., HTTP 200 for a web application, login if applicable)

## Versioning
 The container must have a file last_commits.txt in the WORKDIR. 
    It must include both the commit message and branch, commit hash, user and timestamp. 
    The build workflow must create the file in /tmp, and the Dockerfile COPY it close to the end of the build process.
    The version can be checked with `podman exec <container-name> cat /<WORKDIR>/last_commit.txt`
