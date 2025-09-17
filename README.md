# 🛠️ Workflow: Trigger Review Comment from Token User

📂 Branch: [`workflows/pr-review-comment`](https://github.com/lywebdev/github-workflows/tree/workflows/pr-review-comment)  
📌 Related overview: see [Main page](https://github.com/lywebdev/github-workflows/)

---

## 🎯 Purpose
This workflow automatically adds a review comment to pull requests created by the token user whenever the PR is updated (`synchronize` event).

---

## ⚡ Trigger
- `pull_request` event: `synchronize` — triggered when commits are pushed to an existing PR.

---

## 🔄 Behavior
1. **🔑 Check for `REVIEWER_TOKEN`**
    - ❌ Stops workflow if the secret is missing.

2. **💬 Leave review comment**
    - ✅ Checks if the PR was created by the token user.
    - ✅ If true, posts the comment `@codex make review`.
    - ❌ Skips if the PR was created by another user.

---

## 🔑 Secrets
- `REVIEWER_TOKEN` — required to authenticate as the token user and post the comment.

---

## 📝 Notes
- Only PRs created by the token user are commented on.
- Comments are added only on `synchronize` events, not when a PR is initially opened.  
