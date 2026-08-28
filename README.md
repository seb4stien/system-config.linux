# Linux System Configuration

Scripts and Ansible tasks to configure my Linux environment.

## Structure

- **`bootstrap`**: System initialization script to install core dependencies (Ansible, git, curl, etc.).
- **`playbook.yml`**: Main Ansible playbook divided into privileged system tasks and unprivileged user tasks.
- **`tasks/system/`**: Tasks requiring elevated root privileges (`sudo`), such as `apt` package installation and system configuration (`sshd_config`, `/etc/alternatives`).
- **`tasks/user/`**: Tasks executed as standard user without `sudo`, such as dotfiles (`.bashrc`, `.vimrc`), `dconf` settings, user git configs, and home directory layout.

## Usage

1. Bootstrap dependencies (requires sudo):
   ```bash
   ./bootstrap
   ```
2. Configure options in `inventory.yaml` and `playbook.yml`.
3. Test changes with dry-run:
   ```bash
   ./config-test           # Test all tasks
   ./config-test --user    # Test user tasks only (no sudo required)
   ./config-test --system  # Test system tasks only
   ```
4. Apply configuration:
   ```bash
   ./config-apply          # Apply full configuration
   ./config-apply --user   # Apply user tasks only (no sudo required)
   ./config-apply --system # Apply system tasks only
   ```

## Development & Git Hooks (`prek` / `pre-commit`)

Automated checks are configured using `.pre-commit-config.yaml` (compatible with `prek` or `pre-commit`).

To install Git hooks locally:
```bash
# Using pre-commit
pre-commit install

# Or using prek (Rust drop-in replacement)
prek install
```

To run checks manually on all files:
```bash
pre-commit run --all-files
# or
prek run --all-files
```

## Continuous Integration (CI)

A GitHub Actions workflow ([`.github/workflows/ci.yml`](file://.github/workflows/ci.yml)) runs on every push and pull request to `master` / `main`. It automatically validates:
- YAML syntax, formatting, and file hygiene via `pre-commit`.
- Ansible playbook syntax (`ansible-playbook --syntax-check`).
- Dry-run verification of user environment tasks (`./config-test --user`).

## Conventions

- Aliases related to this tooling should be upper case (e.g. `SC`).
