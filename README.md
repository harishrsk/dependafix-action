# DependaFix - AI PR Comment Resolution Agent 🚀

DependaFix is an autonomous AI Junior Software Engineer that lives in your GitHub Actions. It reads PR review comments, instantly applies the minimal necessary code fixes to the target files, runs your local linters, and commits the fix. Powered by the hyper-fast `gemini-3.5-flash` model via the `google-antigravity` SDK.

## ⚡ Features
- **Zero Collateral Damage**: Makes the minimal changes necessary, matching your existing codebase paradigm.
- **Locality Constraint**: Edits ONLY the files specified in the PR comment.
- **Self-Verifying**: Uses the Antigravity `BashExecution` tool to run your local linters and tests before pushing any code.
- **Graceful Failure**: If the AI's fix breaks your build or validation fails, it automatically aborts and outputs `'AUTOMATED_ABORT: I attempted this fix but it broke validation.'`

## 🛒 How to Buy

DependaFix is a premium Micro-SaaS tool available for a one-time lifetime payment. 

1. **Purchase your Lifetime License** from our secure storefront: https://harishrsk.lemonsqueezy.com/checkout/buy/61892952-c676-4a14-a7a6-c4140ce337ac 
2. After purchase, you will immediately receive a unique `LICENSE_KEY`.
3. Get a Gemini API Key from [Google AI Studio](https://aistudio.google.com/app/apikey).
4. Add both keys to your GitHub Repository Secrets!

## ⚙️ Setup & Installation

1. Go to your GitHub repository -> **Settings** -> **Secrets and variables** -> **Actions**
2. Add the following repository secrets:
   - `GEMINI_API_KEY`
   - `LICENSE_KEY`
3. Create a workflow file in your repo at `.github/workflows/dependafix.yml`:

```yaml
name: DependaFix PR Agent

on:
  issue_comment:
    types: [created]

jobs:
  resolve_pr_comment:
    # Only run on pull requests when someone comments with "@dependafix"
    if: ${{ github.event.issue.pull_request && contains(github.event.comment.body, '@dependafix') }}
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pull-requests: write
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
      
      - name: Run DependaFix Agent
        uses: your-username/dependafix-action@v1 # Replace with your published marketplace action path
        with:
          gemini_api_key: ${{ secrets.GEMINI_API_KEY }}
          github_token: ${{ secrets.GITHUB_TOKEN }}
          license_key: ${{ secrets.LICENSE_KEY }}
```

## 🔒 Security & Privacy (BYOK)
This Action operates in a strict Bring-Your-Own-Key (BYOK) model. Your source code **never** touches our servers. The compiled binary runs entirely within your own GitHub Actions runner, keeping your codebase secure. 

The application logic communicates directly with Google's Gemini API endpoints using your provided API key. The only other external call made is a lightweight license validation check to our Lemon Squeezy endpoint on startup.
