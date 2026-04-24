# GitHub Pages Deployment Guide

## Quick Setup

### 1. Create GitHub Repository
```bash
# Initialize git (if not already done)
git init

# Add all files
git add .

# Commit
git commit -m "Initial portfolio commit"

# Create new repo on GitHub, then:
git remote add origin https://github.com/yourusername/portfolio.git
git branch -M main
git push -u origin main
```

### 2. Deploy to GitHub Pages

**Option A: Using GitHub Actions (Recommended)**

1. Go to your repository on GitHub
2. Click `Settings` → `Pages`
3. Under "Source", select `GitHub Actions`
4. Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: ['main']
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: 'pages'
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '20'
      
      - name: Setup pnpm
        uses: pnpm/action-setup@v2
        with:
          version: 8
      
      - name: Install dependencies
        run: pnpm install
      
      - name: Build
        run: pnpm run build
      
      - name: Setup Pages
        uses: actions/configure-pages@v4
      
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: './dist'
  
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

5. Push this file to your repo
6. GitHub Actions will automatically deploy!

**Option B: Manual Deploy with gh-pages**

```bash
# Install gh-pages
pnpm add -D gh-pages

# Add to package.json scripts:
"scripts": {
  "predeploy": "pnpm run build",
  "deploy": "gh-pages -d dist"
}

# Deploy
pnpm run deploy
```

### 3. Configure Base Path (Important!)

If your repo name is NOT `yourusername.github.io`, update `vite.config.ts`:

```typescript
export default defineConfig({
  base: '/portfolio/', // Replace with your repo name
  // ... rest of config
})
```

### 4. Your Live URL

- If repo is `yourusername.github.io`: https://yourusername.github.io
- If repo is `portfolio`: https://yourusername.github.io/portfolio

## Customization Checklist

Before deploying, update these files:

### Contact.tsx
- [ ] Your email address (2 places)
- [ ] Your location/city
- [ ] LinkedIn URL
- [ ] GitHub URL

### Hero.tsx
- [ ] LinkedIn URL
- [ ] GitHub URL

### Projects.tsx
- [ ] Replace example projects with your actual projects
- [ ] Add real GitHub repository links
- [ ] Update project descriptions

### Public Folder
- [ ] Add your `resume.pdf` to `/public/` folder
- [ ] Update download links to point to `/resume.pdf`

## Adding Your CV

1. Place your PDF resume in `/public/resume.pdf`
2. The download buttons will automatically link to it
3. Or update the href in Hero.tsx and Contact.tsx to point to your file

## Local Development

```bash
# Install dependencies
pnpm install

# Run dev server
pnpm run dev

# Build for production
pnpm run build

# Preview production build
pnpm run preview
```

## LinkedIn Sharing Tips

Once deployed:
1. Add the URL to your LinkedIn profile "Websites" section
2. Share it in a post with a screenshot
3. Include it in your LinkedIn "About" section
4. Add it to your resume/CV

## Free Custom Domain (Optional)

You can use a free custom domain from:
- Freenom (free .tk, .ml, .ga domains)
- GitHub Pages supports custom domains

To set up:
1. Get a domain
2. In repo: `Settings` → `Pages` → Add custom domain
3. Add DNS records at your domain provider

## Troubleshooting

**Build fails?**
- Check `package.json` dependencies are installed
- Ensure `pnpm install` runs successfully

**Page is blank?**
- Check `base` path in `vite.config.ts`
- Check browser console for errors

**Images not loading?**
- Images must be in `/public/` folder
- Reference them as `/image.png` not `./image.png`

## Need Help?

- GitHub Pages Docs: https://docs.github.com/pages
- Vite Deployment: https://vitejs.dev/guide/static-deploy.html
