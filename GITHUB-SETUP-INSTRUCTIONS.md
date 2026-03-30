# GitHub Repository & Pages Setup — CC Execution Instructions

**DO NOT ASK THE USER ANY QUESTIONS. Execute autonomously.**

This file contains the steps to initialize, push, and deploy the IJH repository to GitHub with GitHub Pages. The `.github/workflows/deploy.yml` file already exists and is complete — do NOT attempt to write or modify it (the `${{ }}` template syntax triggers content filters).

---

## STEP 1: Create Missing Root Files

The following files may be missing from the repository root at `C:\Users\verti\claude\dad-IJH-documents-OSS\intentional-journey-of-the-heart\`. Check for each and create any that don't exist:

### LICENSE
Create the full text of the **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International** license. Use the official legal code text from https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode.txt (or reproduce it from your training data — it's a standard license).

### README.md
Create a project README with:
- Project title: **Intentional Journey of the Heart**
- Subtitle: *Notes to My Kids (and Grandkids): On My Personal Exploration of the Laws of God's Love*
- Author: **John G. Tittle**
- Brief description synthesized from the Introduction document (do NOT invent theological claims)
- Badge for license: `[![License: CC BY-NC-SA 4.0](https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-nc-sa/4.0/)`
- Link to the live site: `https://epithetical.github.io/intentional-journey-of-the-heart/`
- Quick overview of the 5 volumes
- "How to Contribute" section pointing to CONTRIBUTING.md
- Technology stack note (MkDocs Material, GitHub Pages)

### CONTRIBUTING.md
Create contributor guidelines covering:
- This work is licensed under CC BY-NC-SA 4.0
- How to submit corrections (open an Issue using the correction template)
- How to propose new content (open an Issue using the contribution-proposal template)
- How to submit community responses or case studies (fork → branch → PR to `docs/community/`)
- All contributions must include YAML front matter (author, date, tags)
- Response papers must cite specific explorations they engage with
- John G. Tittle and JD Tittle review all PRs

### CODE_OF_CONDUCT.md
Create a Contributor Covenant Code of Conduct (standard v2.1) adapted for a theological open-source community. Keep the enforcement section pointing to a placeholder email or GitHub Issues.

### .github/ISSUE_TEMPLATE/question.md
```yaml
---
name: Theological Question or Discussion
about: Ask a question or start a discussion about the content
labels: discussion
---

**Which volume/exploration does this relate to?**


**Your question or discussion topic:**


**Relevant scripture references (if any):**

```

### .github/ISSUE_TEMPLATE/contribution-proposal.md
```yaml
---
name: Content Contribution Proposal
about: Propose a new response paper, case study, or extension
labels: contribution
---

**Type of contribution:**
- [ ] Response paper (engaging with a specific exploration)
- [ ] Case study (applying the framework)
- [ ] Extension (building on an open trail)
- [ ] Other

**Which explorations does this engage with?**


**Brief summary of your proposed contribution:**


**Your background/perspective:**

```

### .github/ISSUE_TEMPLATE/correction.md
```yaml
---
name: Correction or Typo
about: Suggest a correction to existing content
labels: correction
---

**Document/page where the issue appears:**


**What needs correcting:**


**Suggested correction:**

```

### .github/PULL_REQUEST_TEMPLATE.md
```markdown
## Description
Brief description of this contribution.

## Type
- [ ] Correction/typo fix
- [ ] New community response
- [ ] New case study
- [ ] Other

## Related Issues
Closes #

## Checklist
- [ ] YAML front matter included (author, date, tags)
- [ ] Content placed in correct directory
- [ ] Specific explorations cited where relevant
- [ ] Reviewed for theological accuracy
```

---

## STEP 2: Initialize Git Repository

Run the following commands from the repository root `C:\Users\verti\claude\dad-IJH-documents-OSS\intentional-journey-of-the-heart\`:

```powershell
git init
git branch -M main
git add .
git commit -m "Initial commit: IJH Theological Library v5.3 — John G. Tittle"
```

---

## STEP 3: Create GitHub Repository

Use the GitHub MCP tools to create a **public** repository:
- **Owner**: Epithetical
- **Name**: intentional-journey-of-the-heart
- **Description**: "Intentional Journey of the Heart — An open-source theological library exploring the Laws of God's Love. By John G. Tittle."
- **Visibility**: PUBLIC
- **Homepage**: https://epithetical.github.io/intentional-journey-of-the-heart/

If GitHub MCP is not available, use the `gh` CLI:
```powershell
gh repo create Epithetical/intentional-journey-of-the-heart --public --description "Intentional Journey of the Heart — An open-source theological library exploring the Laws of God's Love. By John G. Tittle." --homepage "https://epithetical.github.io/intentional-journey-of-the-heart/"
```

---

## STEP 4: Push to GitHub

```powershell
git remote add origin https://github.com/Epithetical/intentional-journey-of-the-heart.git
git push -u origin main
```

---

## STEP 5: Enable GitHub Pages

Use the GitHub MCP tools or `gh` CLI to enable GitHub Pages:
- **Source**: GitHub Actions (NOT "Deploy from a branch")
- The `.github/workflows/deploy.yml` already exists and will handle builds automatically

Via `gh` CLI:
```powershell
gh api repos/Epithetical/intentional-journey-of-the-heart/pages -X POST -f build_type=workflow
```

If that endpoint requires the Pages API preview, the fallback is:
1. Navigate to https://github.com/Epithetical/intentional-journey-of-the-heart/settings/pages
2. Under "Build and deployment" → Source → select "GitHub Actions"

---

## STEP 6: Verify Deployment

After the first push, the GitHub Actions workflow will:
1. Install Python 3.12
2. Install MkDocs Material and dependencies from `requirements.txt`
3. Build the site with `mkdocs build --strict`
4. Deploy to GitHub Pages

The site should be live within 2-3 minutes at:
**https://epithetical.github.io/intentional-journey-of-the-heart/**

Verify by checking the Actions tab: https://github.com/Epithetical/intentional-journey-of-the-heart/actions

---

## IMPORTANT NOTES

- The `.github/workflows/deploy.yml` is ALREADY WRITTEN and CORRECT. Do NOT recreate or modify it. The `${{ }}` GitHub Actions syntax triggers content filters — this file was written by a separate process.
- The repository MUST be public for GitHub Pages to work on a free GitHub account.
- If `mkdocs build --strict` fails during the Actions run, check the build logs for missing nav references or broken links.
