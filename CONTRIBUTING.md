## Contributing — People Gifting

Thanks for helping with The People Edit. Follow this so any teammate (including new interns) can review your work easily.

### Before you start

1. Read [ONBOARDING.md](./profile/ONBOARDING.md) (org) and the target repo README.
2. Prefer small PRs: one problem → one fix.
3. Never commit `.env`, credentials, or production dumps.

### Branch naming

| Prefix | Use |
|--------|-----|
| `feat/` | New feature |
| `fix/` | Bug fix |
| `docs/` | Documentation only |
| `chore/` | Tooling, deps, cleanup |

### Workflow

```bash
git checkout main
git pull
git checkout -b feat/short-description
# ... make changes ...
git push -u origin HEAD
# open PR on GitHub
```

### PR checklist

- [ ] Title explains **why**, not only what
- [ ] Tested locally (website and/or admin as needed)
- [ ] Screenshots for UI changes
- [ ] Migrations included if schema changed
- [ ] No secrets in the diff

### Code style

- Match existing patterns in the file you edit.
- TypeScript strictness: prefer typed API responses.
- Admin: keep API calls in `src/lib/api.ts` patterns.
- Website: keep Prisma access in server components / route handlers, not the browser.

### Deploy notes

- Website: `npm run build` + `pm2 restart thepeopleedit`
- Admin: `npm run build` with production `VITE_API_URL`; nginx serves `dist/`
- Coordinate DB migrations with whoever owns production
