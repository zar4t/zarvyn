# Naming & Formatting Conventions

I set these conventions to keep the Zarvyn codebase clean, predictable, and easy to maintain as the project grows.

## Files & Folders
- Use lowercase letters with hyphens (`kebab-case`).
- No spaces, accents, or special characters.
- Examples: `threat-model.md`, `audit-log.py`

## Commit Messages
I follow the **Conventional Commits** standard (`type: short description`):
- `feat`: A new feature
- `fix`: A bug fix
- `docs`: Documentation updates
- `chore`: Maintenance, config, or dependency tasks
- `test`: Adding or updating test suites
- `refactor`: Code cleanup that doesn't change behavior or fix bugs
- Example: `feat: add tenant isolation logic`

## Branch Names
- Structure: `<type>/<short-description>`
- Examples:
  - `feature/jwt-auth`
  - `fix/login-error`
  - `docs/update-readme`

## Python Standards
- **Variables & Functions:** `snake_case` (e.g., `tenant_id`, `get_secret()`)
- **Constants:** `UPPER_CASE` (e.g., `MAX_RETRIES`, `SECRET_KEY`)
- **Classes:** `PascalCase` (e.g., `TenantManager`, `SecretVault`)
