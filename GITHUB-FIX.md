# Fix Blank White Page on GitHub Pages

## The Problem
You're seeing a blank white page because the `base` path in `vite.config.ts` doesn't match your GitHub repository name.

## The Solution (Choose One)

### Option 1: Your repo is `username.github.io`

**Update `vite.config.ts` line 10:**
```typescript
base: '/',
```

**Your site will be at:**
```
https://username.github.io/
```

### Option 2: Your repo has a custom name (e.g., "portfolio")

**Update `vite.config.ts` line 10:**
```typescript
base: '/portfolio/', // ← Use YOUR actual repo name
```

**Examples:**
- Repo: `github.com/john/portfolio` → `base: '/portfolio/'`
- Repo: `github.com/john/my-site` → `base: '/my-site/'`
- Repo: `github.com/john/nav-arch` → `base: '/nav-arch/'`

**Your site will be at:**
```
https://username.github.io/portfolio/
```

## How to Check Your Repo Name

1. Go to your GitHub repository
2. Look at the URL: `github.com/USERNAME/REPO-NAME`
3. The part after your username is your repo name
4. Use that in `base: '/REPO-NAME/'`

## Quick Fix Steps

1. **Find your repo name** from GitHub URL
2. **Update `vite.config.ts`** with correct base path
3. **Rebuild and push:**
   ```bash
   git add vite.config.ts
   git commit -m "Fix base path for GitHub Pages"
   git push
   ```
4. **Wait 2-3 minutes** for GitHub Actions to rebuild
5. **Visit your site** - should work now! ✅

## Why This Happens

When you deploy to GitHub Pages:
- GitHub serves your site at `username.github.io/REPO-NAME/`
- Vite needs to know this path to load assets correctly
- If the `base` path is wrong, the browser can't find your CSS/JS files
- Result: blank white page (check browser console - you'll see 404 errors)

## Test Locally First

Before pushing, test your build locally:

```bash
# Build with your updated base path
pnpm run build

# Preview it
pnpm run preview

# Visit http://localhost:4173
# Should look correct!
```

## Enable GitHub Pages

Make sure GitHub Pages is enabled:

1. Go to your repo → **Settings** → **Pages**
2. Under **Source**, select **GitHub Actions**
3. Save

## Common Mistakes

❌ **Wrong:**
```typescript
base: 'portfolio'      // Missing slashes
base: '/portfolio'     // Missing trailing slash
base: '/Portfolio/'    // Wrong case (case-sensitive!)
```

✅ **Correct:**
```typescript
base: '/portfolio/'    // Exact repo name with slashes
```

## Still Blank?

**Check browser console (F12):**
- See 404 errors for CSS/JS files? → Base path is still wrong
- See CORS errors? → Rare, but check HTTPS settings
- No errors but blank? → Check React errors in console

**Check GitHub Actions:**
- Go to **Actions** tab in your repo
- Latest workflow should be green ✅
- If red ❌, click to see error logs

**Check GitHub Pages settings:**
- Settings → Pages
- Should show: "Your site is live at..."
- If not, source should be "GitHub Actions"

## Example: Complete Fix

**My repo is: `github.com/john/portfolio`**

**Step 1: Update vite.config.ts**
```typescript
base: '/portfolio/',
```

**Step 2: Commit and push**
```bash
git add vite.config.ts
git commit -m "Fix GitHub Pages base path"
git push
```

**Step 3: Wait for Actions to complete**
- Check **Actions** tab for green checkmark

**Step 4: Visit site**
```
https://john.github.io/portfolio/
```

Done! ✅

## Pro Tip: Environment Variables

For multiple deployment targets, use environment variables:

```typescript
// vite.config.ts
export default defineConfig({
  base: process.env.VITE_BASE_PATH || '/',
  // ...
})
```

Then set in GitHub Actions:
```yaml
- name: Build
  run: pnpm run build
  env:
    VITE_BASE_PATH: /portfolio/
```

## Need More Help?

1. Check browser console for errors (F12)
2. Check GitHub Actions logs
3. Verify repo name matches base path exactly
4. Try `base: '/'` as a test (works for all cases but breaks assets on project pages)
