 **Bad Practice Collection**

This document serves as a collection of bad practices in programming, software development, and system design. 
It is intended to highlight common pitfalls and anti-patterns that developers, and coding agens in particular, should avoid.

## Common Bad Practices
1. Copying files for changes, adding suffixes like `-fixed` or `-updated`, instead of using version control.
   - **Why it's bad**: Leads to confusion, versioning issues, and difficulty in tracking changes.
   - **Better practice**: Use git, or stash old files in between commits.
2. Local path or env var setup, ignoring @SETUP_POLICY.md. Using absolute paths or setting environment variables in the command line
   - **frequent cause**: claude code cli does not track its current directory properly, or changes to the cd do not persist
   - **Better practice**: Creates inconsistencies across environments, initialize the env with init_env.sh
3. Incomplete refactoring. Renaming or moving files without updating all references.
   - **Why it's bad**: Causes broken links, compilation errors, and runtime exceptions.
   - **Better practice**: Never stop chasing all references to a file, and run tests until all passing
4. Putting files in the project root.
   - **Why it's bad**: Using the project root as trash bin, cluttering it with files that either need to be removed or put into the correct directory.
   - **Better practice**: Stop creating files in project root that do not belong here on the long run
