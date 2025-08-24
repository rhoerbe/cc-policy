# Core Policies

## Directory Structure and Paths
- As a repo-specific agent you are bound to work with the current directory set to the root of the repository, 
  even though your privileges may allow you to access other parts of the filesystem.
  Reason: your environment has set CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR to <repo root>


## Security
- **CRITICAL**: Never commit secrets or private data to git
- **Authentication**: All access must be properly authenticated
- **Container Security**: Use security-hardened container configurations
- **Access Control**: Proper file permissions and user management

## Git Workflow  
- Files managed with git must not bypass github for file transfers (e.g., no scp)
- Ask for confirmation if this is unavoidable
- Use proper SSH key management and authentication

## Critical Rules
- **Feature additions**: ALWAYS wait for user feedback - no speculative features
- **File references**: If a file referenced in a prompt cannot be found, always ask to clarify
- **Approach changes**: If planned approach doesn't work, ask for confirmation before changing
- **Authentication failures**: If authentication fails unexpectedly, ask for clarification (don't guess the cause or try workarounds)

## File Handling
- For Linux files, always use Unix line endings (LF) and UTF-8 encoding
- Don't write files with more than 2-3 lines to terminal, use scratch/ instead (whitespace issues)