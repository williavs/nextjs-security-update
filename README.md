# nextjs-security-update

There are people building OSS tools to exploit the new Next.js vulnerabilities. This is a tool to fight back - makes it dumb easy to upgrade all your Next.js apps to versions that won't get you hacked.

## What happened

Dec 11, 2025: Next.js disclosed CVE-2025-55183 (source code exposure) and CVE-2025-55184/CVE-2025-67779 (DoS). If you're running React Server Components with App Router, you're affected.

https://nextjs.org/blog/cve-2025-55183-and-cve-2025-55184

## What this does

1. Discovers all your GitHub accounts (personal + orgs)
2. Lets you pick which ones to scan
3. Finds every Next.js repo
4. Upgrades package.json to the correct patched version
5. Commits locally (you push when ready)

## Usage

```bash
curl -O https://raw.githubusercontent.com/williavs/nextjs-security-update/main/nextjs-security-update.sh
chmod +x nextjs-security-update.sh
./nextjs-security-update.sh
```

Or specify accounts directly:

```bash
./nextjs-security-update.sh myusername myorg
```

## Options

```bash
DRY_RUN=true ./nextjs-security-update.sh    # See what would change
AUTO_PUSH=true ./nextjs-security-update.sh  # Push automatically
```

## Requirements

- `gh` (GitHub CLI) - authenticated
- `jq`
- `git`

## Version mapping

| From | To |
|------|-----|
| 13.x, 14.0.x, 14.1.x, 14.2.x | 14.2.35 |
| 15.0.x | 15.0.7 |
| 15.1.x | 15.1.11 |
| 15.2.x | 15.2.8 |
| 15.3.x | 15.3.8 |
| 15.4.x | 15.4.10 |
| 15.5.x | 15.5.9 |
| 15.x canary | 15.6.0-canary.60 |
| 16.0.x | 16.0.10 |
| 16.x canary | 16.1.0-canary.19 |

## After running

Push all changes:
```bash
cd ~/nextjs-security-updates
for d in */; do (cd "$d" && git push && echo "Pushed $d"); done
```

Then run `npm install` in each project and redeploy.
