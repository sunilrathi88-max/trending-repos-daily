# 🔥 Trending Repos Daily

Automated GitHub Actions workflow that finds the top 5 trending repositories on GitHub and sends them via email daily at 10:00 AM IST.

## 🚀 Features

- **Automated Daily Emails**: Sends trending repos every day at 10 AM IST (4:30 AM UTC)
- **Top 5 Trending**: Fetches repositories created in the last 24 hours, sorted by stars
- **Rich HTML Emails**: Beautifully formatted emails with repository details
- **Manual Trigger**: Can be manually triggered via GitHub Actions UI

## ⚙️ Setup Instructions

### Step 1: Fork or Clone This Repository

You can fork this repository or use it as a template.

### Step 2: Set Up Email Secrets

You need to configure three secrets for the email functionality:

1. Go to your repository **Settings**
2. Navigate to **Secrets and variables** > **Actions**
3. Click **New repository secret**
4. Add the following three secrets:

#### Required Secrets:

**1. EMAIL_USERNAME**
- Your Gmail address (e.g., `yourname@gmail.com`)
- This will be used to send emails via SMTP

**2. EMAIL_PASSWORD**
- Your Gmail App Password (NOT your regular Gmail password)
- **How to generate Gmail App Password:**
  1. Go to your Google Account settings
  2. Navigate to Security
  3. Enable 2-Factor Authentication (if not already enabled)
  4. Go to "App passwords" under Security
  5. Generate a new app password for "Mail"
  6. Copy the 16-character password (remove spaces)
  7. Use this as your EMAIL_PASSWORD secret

**3. EMAIL_TO**
- The email address where you want to receive the trending repos
- Can be the same as EMAIL_USERNAME or different
- Example: `yourname@gmail.com`

### Step 3: Test the Workflow

Once secrets are configured:

1. Go to the **Actions** tab in your repository
2. Click on "Daily Trending Repos Email" workflow
3. Click **Run workflow** > **Run workflow** button
4. Wait for the workflow to complete (usually takes 10-20 seconds)
5. Check your email inbox for the trending repos!

### Step 4: Customize (Optional)

#### Change Schedule Time
Edit `.github/workflows/main.yml` and modify the cron expression:
```yaml
schedule:
  - cron: '30 4 * * *'  # 4:30 AM UTC = 10:00 AM IST
```

#### Change Number of Repositories
Edit the `per_page` parameter in the workflow file:
```bash
"https://api.github.com/search/repositories?q=created:>$DATE&sort=stars&order=desc&per_page=5"
```
Change `per_page=5` to any number you want.

#### Use Different Email Provider
If you want to use a different email provider (not Gmail), update:
- `server_address`: Your SMTP server
- `server_port`: Your SMTP port

## 💬 How It Works

1. **Scheduled Trigger**: GitHub Actions runs automatically at 10 AM IST every day
2. **Fetch Trending Repos**: Uses GitHub's Search API to find repos created in the last 24 hours
3. **Sort by Stars**: Orders results by star count (descending)
4. **Format Email**: Creates a beautiful HTML email with repo details
5. **Send Email**: Uses SMTP to send the email to your configured address

## 📧 Email Content

The email includes for each repository:
- Repository name with clickable link
- Star count ⭐
- Description 📝
- Programming language 🔤

## 🔧 Troubleshooting

### Workflow Fails with "Authentication Failed"
- Make sure you're using a Gmail **App Password**, not your regular password
- Verify that 2FA is enabled on your Google account
- Double-check that the EMAIL_USERNAME and EMAIL_PASSWORD secrets are correct

### Not Receiving Emails
- Check your spam/junk folder
- Verify the EMAIL_TO secret is correct
- Run the workflow manually to test

### Workflow Runs But No Trending Repos
- GitHub API might be rate-limited
- No new repositories with significant stars in the last 24 hours

## 📝 License

Free to use and modify!

## 🚀 Contributing

Feel free to open issues or submit PRs to improve this workflow!

---

**Built with ❤️ using GitHub Actions**
