# Quick Start: Deploy to GitLab Pages

## ✅ Your app is ready! Here's what to do:

### 1. Update Configuration (2 minutes)

**Edit `vite.config.ts`:**
```typescript
base: '/your-repo-name/', // ← Change to YOUR GitLab repo name
```

Example:
- Repo: `gitlab.com/john/portfolio` → Use `base: '/portfolio/'`
- Repo: `gitlab.com/john/john.gitlab.io` → Use `base: '/'`

### 2. Add Your Content (5 minutes)

1. **Update contact info** in:
   - `src/app/components/Hero.tsx`
   - `src/app/components/Contact.tsx`

2. **Add your files** to `/public/`:
   - `resume.pdf` - Your CV
   - `projects/` - Project screenshots
   - `reports/` - PDF reports

3. **Update projects** in `src/app/components/Projects.tsx`

### 3. Deploy to GitLab (3 minutes)

```bash
# Create a new repo on GitLab (e.g., "portfolio")

# In your terminal:
git init
git add .
git commit -m "Naval architecture portfolio"
git remote add origin https://gitlab.com/YOUR-USERNAME/portfolio.git
git branch -M main
git push -u origin main
```

### 4. Wait for Build (2 minutes)

- GitLab will automatically build your site using `.gitlab-ci.yml`
- Check progress: **Your Repo** → **CI/CD** → **Pipelines**
- Wait for green checkmark ✅

### 5. Visit Your Site!

Your portfolio will be live at:
```
https://YOUR-USERNAME.gitlab.io/portfolio/
```

## That's It! 🚀

Total time: **~12 minutes**

## What Just Happened?

1. GitLab ran `pnpm install` and `pnpm run build`
2. Your React app was compiled to static HTML/CSS/JS
3. GitLab Pages served the files from the `dist` folder
4. **No Node.js needed** - it's just plain HTML now!

## Next Steps

- [ ] Share the link on LinkedIn
- [ ] Add custom domain (optional)
- [ ] Update with real project data
- [ ] Add your actual resume PDF

## Need Help?

- Full guide: See `GITLAB-DEPLOYMENT.md`
- Assets guide: See `ASSETS-GUIDE.md`
- Local testing: `pnpm run build && pnpm run preview`

---

**Pro Tip:** Your React app builds to 100% static HTML/CSS/JS. GitLab Pages, GitHub Pages, Netlify, Vercel - they all work the same way. You're not locked into GitLab!
