# GitHub Push Instructions for OpenClawPM

The OpenClawPM MVP codebase is built and ready to be pushed to GitHub. Follow these steps:

## Step 1: Create GitHub Repository

1. Go to https://github.com/new
2. Fill in:
   - **Repository name**: `openclawpm`
   - **Description**: "Managed SaaS platform for property management companies to deploy and manage OpenClaw instances"
   - **Visibility**: Private (or Public if you prefer)
   - **Initialize repository**: NO (don't add README, .gitignore, or license - we have these)
3. Click **Create repository**

## Step 2: Get Your GitHub Authentication Ready

You'll need one of these methods:

### Option A: SSH Key (Recommended)
If you haven't set up SSH keys:
```bash
# Check if you have SSH keys
ls ~/.ssh/id_rsa

# If not, generate one
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# Copy the public key
cat ~/.ssh/id_rsa.pub
```

1. Go to GitHub → Settings → SSH and GPG keys
2. Click "New SSH key"
3. Paste your public key
4. Save

Then use SSH URL for remote: `git@github.com:bramscher/openclawpm.git`

### Option B: Personal Access Token
1. Go to GitHub → Settings → Developer settings → Personal access tokens
2. Click "Tokens (classic)" or "Fine-grained tokens"
3. Create new token with `repo` scope
4. Copy the token
5. When pushing, use: `https://YOUR_TOKEN@github.com/bramscher/openclawpm.git`

### Option C: GitHub CLI
If you have `gh` CLI installed:
```bash
gh auth login
# Follow the prompts
```

## Step 3: Push the Code

Navigate to the codebase directory and push:

```bash
cd /home/node/.openclaw/workspace/openclawpm-codebase

# Verify the remote is set correctly
git remote -v
# Should show: origin	https://github.com/bramscher/openclawpm.git

# If remote needs to be updated:
git remote remove origin
git remote add origin https://github.com/bramscher/openclawpm.git
# OR (for SSH)
git remote add origin git@github.com:bramscher/openclawpm.git

# Push to GitHub
git push -u origin main
```

If using Personal Access Token:
```bash
git push -u origin main
# Enter username: your-github-username
# Enter password: your-personal-access-token
```

## Step 4: Verify on GitHub

1. Go to https://github.com/bramscher/openclawpm
2. Verify all files are there:
   - app/ (all pages and API routes)
   - lib/ (Supabase configuration)
   - docs/ (schema and setup guide)
   - package.json (dependencies)
   - README.md (documentation)
   - etc.

3. Check commit history shows your initial commit

## Step 5: Add Collaborators (Optional)

If you want to add team members:
1. Go to repository → Settings → Collaborators
2. Click "Add people"
3. Enter their GitHub username
4. Select permission level (Write for team members)

## Step 6: Set Up Branch Protection (Optional but Recommended)

1. Go to repository → Settings → Branches
2. Click "Add rule" under "Branch protection rules"
3. Pattern: `main`
4. Check:
   - "Require a pull request before merging"
   - "Require status checks to pass before merging"
5. Save

## Troubleshooting

### "fatal: could not read Username for 'https://github.com'"
**Solution**: Use SSH key method instead or enter credentials when prompted.

### "Repository not found"
**Solution**: 
- Verify you created the repository on GitHub
- Check repository name is exactly: `openclawpm`
- Check account is: `bramscher`
- Verify it's not in a different organization

### "Permission denied (publickey)"
**Solution**: Your SSH key isn't set up correctly. Use Personal Access Token method instead.

### "Updates were rejected because the remote contains work"
**Solution**: The repository already has files. Either:
- Delete and recreate the empty repository
- Or pull first: `git pull origin main`

## After Push

You can now:

1. **Deploy to Vercel**
   - Go to https://vercel.com
   - Click "New Project"
   - Select your GitHub repository
   - Add environment variables
   - Deploy

2. **Enable CI/CD** (optional)
   - Add GitHub Actions workflows
   - Set up automated testing
   - Configure auto-deploy on push

3. **Manage Issues & PRs**
   - GitHub issues for bug tracking
   - Pull requests for code review
   - Discussions for questions

4. **Set Up Releases**
   - Tag versions with `git tag v0.1.0`
   - Create releases on GitHub
   - Include changelog

## Quick Commands Reference

```bash
# Navigate to project
cd /home/node/.openclaw/workspace/openclawpm-codebase

# Check git status
git status

# View commit history
git log --oneline

# Show what will be pushed
git log origin/main..main

# Push changes
git push origin main

# Create new branch for development
git checkout -b feature/your-feature-name
git push -u origin feature/your-feature-name

# Create pull request on GitHub (web)
# Go to repository → Pull requests → New pull request

# Delete local branch after merge
git branch -d feature/your-feature-name

# Force push (only if you know what you're doing!)
git push -f origin main
```

## Git Configuration

These are already set up in the repo:
- Branch: main
- Author: OpenClawPM Developer (dev@openclawpm.com)
- Initial commit with full codebase

## Documentation for Team

Once pushed, the team can:

1. **Clone the repository**
   ```bash
   git clone https://github.com/bramscher/openclawpm.git
   cd openclawpm
   npm install
   ```

2. **Set up development**
   - Follow `docs/SETUP.md`
   - Create `.env.local` with Supabase credentials
   - Run `npm run dev`

3. **Make changes**
   - Create feature branch
   - Make commits
   - Push and create PR
   - Merge after review

4. **Deploy**
   - Vercel auto-deploys from main
   - Or manually trigger Vercel build

---

**Next Step**: Follow the steps above to push to GitHub, then proceed with Supabase setup and deployment to Vercel.

For any issues, check the README.md or docs/SETUP.md for detailed troubleshooting.
