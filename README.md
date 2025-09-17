# Workflow: Trigger Review Comment from Token User

📂 Branch: [`workflows/pr-review-comment`](https://github.com/lywebdev/github-workflows/tree/pr-review-comment)  
📌 Related overview: see [Main page](https://github.com/lywebdev/github-workflows/)

## Description

This workflow automatically adds a review comment to pull requests created by the token user whenever the PR is updated (`synchronize` event).

### Trigger

The workflow runs on the `pull_request` event with the type:

- `synchronize` — triggered when commits are pushed to an existing PR.

### Jobs

#### `comment-on-update`

- **Runs on:** `ubuntu-latest`
- **Steps:**
    1. **Check for `REVIEWER_TOKEN`**  
       Ensures the secret token exists before proceeding.
    2. **Leave review comment**
        - Checks if the PR was created by the token user.
        - If true, posts a comment `@codex make review`.
        - Skips if the PR was created by another user or if the token is missing.

### Secrets

- `REVIEWER_TOKEN` — required to authenticate as the token user and post the comment.

### Notes

- Only PRs created by the token user are commented on.
- Comments are added only on `synchronize` events, not when a PR is initially opened.
