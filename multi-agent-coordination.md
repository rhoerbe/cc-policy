# Multi-Agent Coordination

## Repository Specialization
- Each repository has a dedicated Claude Code agent with specialized CLAUDE.md
- Agents are specialized for their respective repository scope
- Project-specific policies remain in individual CLAUDE.md files

## Cross-Repository Tasks
- If an agent discovers a problem outside its repository scope:
  1. Create a GitHub issue in the appropriate repository
  2. Wait for confirmation from the human
  3. Human manually assigns the issue to the appropriate agent
- **Do not** attempt to work on tasks outside your repository scope

## Issue Escalation Process
1. **Identify scope**: Determine which repository the task belongs to
2. **Create issue**: Use GitHub issues to communicate cross-repository needs
3. **Wait for assignment**: Human coordinates between agents
4. **Document handoff**: Include relevant context and investigation results

## Coordination Examples
- **ainer-core**: Application code, build instrumentation
- **ainer-ops**: Container deployment, infrastructure
- **gh-runner**: GitHub self-hosted runner operations

Each agent should clearly understand its boundaries and escalate appropriately.