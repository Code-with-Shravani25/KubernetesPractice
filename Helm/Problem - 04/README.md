# Rollback a Helm release
---
- If something goes wrong after upgrade, you can rollback to a previous version.
## Step 1: Check release history
```bash
helm history my-nginx
```
## Step 2: Rollback to previous version
```bash
helm rollback my-nginx 1
```
- Revert the Helm release my-nginx back to revision 1 (a previous version of the deployment).
