# 📋 Workspace Rules & Safety Checklist

Hey team! To keep our pipelines green and prevent accidental production crashes, we have fully automated our repository guardrails. Please review these mandatory guidelines and sync your local machine.

---

### 🔄 Pull Request & Merging Protocol
* **No Red Merges:** You cannot merge a PR if the status checks are red. The GitHub interface will physically lock out the merge button until your code complies with all workspace rules.
* **Keep Up to Date:** Before opening a PR or clicking merge, you must pull the latest changes from the target branch (`dev`) into your feature branch to prevent silent integration failures.
* **Bypass Restrictions:** Admin bypass rules are for emergency overrides only. Do not ask for or attempt code merges that bypass the active CI/CD check suites.

---

### 📂 File & Directory Rules
* **Root Folder Structure:** Move `package.json` and your lockfiles completely inside the `/frontend` folder. Nothing goes in the root.
* **Shared Space:** Keep the shared contract as a single file directly at `shared/api-contract.ts`. Delete any nested folders inside `/shared`.
* **Environment Variables:** If you add any new environment variables, remember to add them as blank keys inside `frontend/.env.example` or `backend/.env.example`. Missing templates will immediately fail the build.

---

### 🟢 Node Version Lock
* **Strict Versioning:** Do not change the engine settings. We are strictly locked to **Node 20** across our workflows and local workspaces. Upgrading to Node 22 or any unverified version locally will trigger an immediate Frontend/Backend CI execution crash.

---

### 🌿 Branching & Git Strategy
* **Branch Naming:** All development work must take place on isolated feature branches using the `feature/*` naming layout (e.g., `feature/store-app-fix`).
* **Protected Branches:** Direct pushes or unreviewed merges to both `main` and `dev` are permanently blocked by GitHub rulesets. Everything must pass through a PR with verified status checks.

---

### 🔒 Default Database Security
Because we enforced an automatic RLS trigger, never push a table migration without its security policies written inside that same file. 

**Separated Permissions Strategy:**
1. **Public:** Can only READ (use `FOR SELECT`).
2. **Authenticated Internal Team:** Can WRITE/EDIT (use `FOR ALL TO authenticated`).

*This keeps our data 100% safe and stops '403 Forbidden' integration errors on the frontend!*

---

### ⚠️ Action Required: Update your Local Setup

Open your terminal and run these commands to pull down the new configurations and activate the automated pre-commit guards on your machine:

```bash
git checkout dev && git pull origin dev
cd frontend
npm install


Once you run this, your local terminal will automatically help you catch things like misplaced lockfiles or accidental secret exposures before you commit your code.

**Let me know if you run into any issues with the setup!**
