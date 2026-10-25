# Publish a website release

Source and release assets: `nishkodotco/app.xponent.site` (private).
Public hosting: `nishkodotco/xponent`.

One-time GitHub setup:

1. Set this repository's Pages publishing source to **GitHub Actions**.
2. Add `XPO_SITE_READ_TOKEN` as a repository Actions secret: use a fine-grained token restricted to `app.xponent.site`, with **Contents: read**. The public repository's default token cannot read another private repository.
3. Configure the `PRD` environment with the desired reviewers and deployment branch rules. Declaring an environment in YAML does not enable approvals by itself; reviewer availability depends on the GitHub plan.
4. Configure the custom domain `xponent.app` in Pages and its DNS, if not already configured.

To deploy, run **Publish Xponent website** from Actions, entering the exact semantic version (initially `0.0.0`). The workflow downloads the static release, checks its SHA-256 checksum and version, and deploys it after any configured PRD approval. It does not copy private source or credentials into the public repository.

To roll back the landing page, run the workflow again with an earlier release version. This changes static hosting only, not Supabase data.
