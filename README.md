# 🚀 GitHub Workflows for Pull Request Automation

This repository contains two GitHub Actions workflows designed to automate PR management and review processes ✨

---

## 1. [`workflows/pr-reassigning.yml`](https://github.com/lywebdev/github-workflows/tree/workflows/pr-reassigning) – Recreate PR Under Token User 🛠️

### 🎯 Purpose
Automatically recreates pull requests under a designated token user (`REVIEWER_TOKEN`) to standardize PR ownership and ensure proper review flow.

### ⚡ Trigger
- `pull_request` events: `opened`, `review_requested`

### 🔄 Behavior
- Checks if the PR author is different from the token user.
- Closes the original PR safely. ✅
- Creates a new PR under the token user with the same title, body, base, and head branch.
- Copies assignees and reviewers from the original PR, excluding the token user to prevent errors. 🧹
- Adds comments to both old and new PRs documenting the recreation. 📝
- Prevents duplicate PRs for the same branch by the token user. 🚫

### 🔑 Requirements
- Repository secret: `REVIEWER_TOKEN`
- Original PR must have reviewers assigned.

---

## 2. [`workflows/pr-review-comment.yml`](https://github.com/lywebdev/github-workflows/tree/workflows/pr-review-comment) – Trigger Review Comment from Token User 💬

### 🎯 Purpose
Automatically leaves a review comment (`@codex make review`) on a PR whenever the token user updates it, to prompt the review process.

### ⚡ Trigger
- `pull_request` event: `synchronize` (i.e., when new commits are pushed to an open PR)

### 🔄 Behavior
- Checks if the PR was created by the token user.
- If true, leaves a comment `@codex make review` after each update. ✍️
- Safely exits if `REVIEWER_TOKEN` is not set or the PR was created by another user. 🚪

### 🔑 Requirements
- Repository secret: `REVIEWER_TOKEN`

---

## 📝 Notes
- Both workflows rely on a `REVIEWER_TOKEN` to perform actions under a bot/user account.
- `pr-reassigning` ensures standardized PR ownership and prevents errors when assigning reviewers.
- `pr-review-comment` ensures the token user automatically prompts reviews after updates.
