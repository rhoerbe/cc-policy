# cc-policy

Common Claude Code agent policies and coordination rules for multi-repository projects.

## Structure

- `core-policies.md` - Security, git workflow, and critical operational rules
- `claude-interaction.md` - Communication standards and reporting guidelines  
- `multi-agent-coordination.md` - Cross-repository collaboration patterns
- `definition-of-done.md` - Quality standards and verification requirements

## Usage

Include in project CLAUDE.md files:

```markdown
## Common Policies
Follow policies in: `file:///mnt/c/Users/r2h2/devl/cc-policy/`
- [Core Policies](file:///mnt/c/Users/r2h2/devl/cc-policy/core-policies.md)
- [Interaction Standards](file:///mnt/c/Users/r2h2/devl/cc-policy/claude-interaction.md)
- [Multi-Agent Coordination](file:///mnt/c/Users/r2h2/devl/cc-policy/multi-agent-coordination.md)
- [Definition of Done](file:///mnt/c/Users/r2h2/devl/cc-policy/definition-of-done.md)
```

This centralizes non-project-specific policies while keeping project context local.