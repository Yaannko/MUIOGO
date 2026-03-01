# Troubleshooting MUIOGO Setup

This guide addresses common issues encountered during the setup and execution of MUIOGO.

## macOS (Apple Silicon / Intel) Common Issues

### Homebrew Permission Errors
When running `./scripts/setup.sh`, you may encounter an error message stating that `/opt/homebrew` is not writable. This prevents the script from automatically installing the required solvers (`glpk` and `cbc`).

**Error Message Example:**
```text
Error: /opt/homebrew is not writable. You should change the ownership and permissions of /opt/homebrew back to your user account.
```

**Resolution:**
1. Open your terminal.
2. Run the following command to fix the permissions (you will be prompted for your Mac password):
   ```bash
   sudo chown -R $(whoami) /opt/homebrew
   ```
3. After fixing permissions, manually install the solvers:
   ```bash
   brew install glpk cbc
   ```
4. Verify the installation:
   ```bash
   glpsol --version
   cbc --version
   ```

### Python 3.11 Not Found
MUIOGO requires Python 3.11 specifically. If you have other versions installed, the setup script may fail.

**Resolution:**
Install Python 3.11 using Homebrew:
```bash
brew install python@3.11
```

## Solver Verification

If the application starts but model runs fail, ensure the solvers are in your system's PATH. You can check this by running:
```bash
which glpsol
which cbc
```
If these commands do not return a path, please install them manually as described in the [Requirements](../README.md#requirements) section.
