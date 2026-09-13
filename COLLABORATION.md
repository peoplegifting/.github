# Collaboration & org setup

This org follows GitHub’s recommended “getting started” checklist.

## Invite your people

1. Open https://github.com/orgs/peoplegifting/people  
2. **Invite member** → GitHub username or email  
3. Add them to the **Developers** team (write access to product repos)

Base permission for all members: **Read**.  
Write access is granted via the **Developers** team.

```bash
# Or via CLI (org admin):
gh api -X PUT orgs/peoplegifting/teams/developers/memberships/USERNAME -f role=member
gh api -X PUT orgs/peoplegifting/invitations -f email='person@example.com' -f role='direct_member'
```

## Customize members’ permissions

| Setting | Value |
|---------|--------|
| Default repository permission | `read` |
| Create repositories | disabled for members |
| Developers team | `write` on PeopleGifting + PeopleGifting-Admin |

## Collaborative coding

### Create a pull request

```bash
git checkout -b feat/my-change
# ... commit ...
git push -u origin HEAD
gh pr create --title "feat: …" --body "…"
```

Templates live in each repo under `.github/PULL_REQUEST_TEMPLATE.md`.

### Branch protection (requires GitHub Pro on private repos)

On the **free** org plan, GitHub blocks branch protection / rulesets for **private** repositories.

When you upgrade to **Team/Pro**, enable on `main` for both product repos:

- Require a pull request before merging  
- Dismiss stale reviews  
- Require status checks: **Lint & build** / **Typecheck & build**  
- Do not allow force pushes / deletions  

UI: **Settings → Branches → Add branch protection rule** → `main`.

Until then: treat `main` as protected by policy (PRs only; no direct pushes except emergencies).

## Automation and CI/CD

| Workflow | Repo | Trigger |
|----------|------|---------|
| `CI` | PeopleGifting | push/PR → lint + prisma migrate + build |
| `CI` | PeopleGifting-Admin | push/PR → typecheck + build |
| `Auto-assign issues` | both | new issue → assign `@harshalDharpure` + `triage` label |
| Dependabot | both | weekly npm / monthly Actions |

Actions:  
https://github.com/peoplegifting/PeopleGifting/actions  
https://github.com/peoplegifting/PeopleGifting-Admin/actions  

## CODEOWNERS

Both repos list `@harshalDharpure` in `.github/CODEOWNERS` for review routing.
