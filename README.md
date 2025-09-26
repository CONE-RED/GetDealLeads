# GetDeal.ai QR Landing Page - Deployment Instructions

## Files Created

1. **index.html** - The landing page (ready for Netlify)
2. **n8n-workflow.json** - Complete n8n workflow for automation

## Quick Deploy Steps (15 minutes)

### Step 1: Deploy to Netlify (5 minutes)

1. Create GitHub repo and push files:
```bash
git init
git add .
git commit -m "Initial GetDeal.ai landing page"
git remote add origin YOUR_GITHUB_REPO_URL
git push -u origin main
```

2. Deploy on Netlify:
   - Go to [Netlify](https://netlify.com)
   - Click "Add new site" → "Import an existing project"
   - Connect GitHub → Select your repo
   - Deploy! You'll get a URL like `amazing-curie-123.netlify.app`

### Step 2: Set up n8n Workflow (10 minutes)

1. Sign up at [n8n.cloud](https://n8n.cloud)
2. Import the workflow:
   - Copy content from `n8n-workflow.json`
   - In n8n, create new workflow → Import from clipboard

3. Configure the nodes:

#### A. Google Sheets Node:
   - Create a Google Sheet with these columns:
     ```
     A: timestamp | B: name | C: email | D: organization | E: role 
     F: focus | G: checkSize | H: analysis | I: dealFlow | J: teamAcquisition 
     K: portfolioSynergy | L: syndication | M: startupUrl | N: challenge | O: source
     ```
   - Copy the Google Sheet ID from URL
   - Replace `YOUR_GOOGLE_SHEET_ID_HERE` in the workflow
   - Connect your Google account

#### B. Email Node:
   - Set up SMTP credentials (Gmail recommended)
   - The workflow includes a complete welcome email template

#### C. Webhook Node:
   - After saving, n8n will provide a webhook URL
   - Copy this URL

### Step 3: Update HTML with Webhook URL (2 minutes)

1. Open `index.html`
2. Find line 727:
   ```javascript
   const response = await fetch('https://YOUR-N8N-INSTANCE.n8n.cloud/webhook/getdeal-qualifier', {
   ```
3. Replace `YOUR-N8N-INSTANCE.n8n.cloud` with your actual n8n webhook URL
4. Redeploy to Netlify (just push to git)

### Step 4: Generate QR Code (1 minute)

1. Use any QR code generator
2. Enter your Netlify URL
3. Download and test!

## Form Data Structure

The form sends this JSON to n8n:
```javascript
{
  "timestamp": "2024-01-01T12:00:00.000Z",
  "source": "qr_code_lead",
  "name": "John Smith",
  "email": "john@example.com", 
  "organization": "Venture Partners LLC",
  "role": "angel",
  "focus": "AI infrastructure",
  "checkSize": "50-250k",
  "services": {
    "analysis": true,
    "dealFlow": false,
    "teamAcquisition": true,
    "portfolioSynergy": false,
    "syndication": false
  },
  "startupUrl": "https://startup.com",
  "challenge": "Need faster due diligence"
}
```

## Testing Checklist

- [ ] Form submits successfully
- [ ] Data appears in Google Sheets
- [ ] Welcome email is sent
- [ ] QR code works on mobile
- [ ] Success page displays
- [ ] Error handling works

## Monitoring

Check these metrics in Google Sheets:
- Total leads: `=COUNTA(B:B)-1`
- Conversion rate by step
- Service selection patterns
- URL provision rate

## Support

If you encounter issues:
1. Check n8n workflow execution logs
2. Verify webhook URL is correct
3. Test with browser DevTools Network tab
4. Check SMTP settings for email delivery

---

**Total deployment time: 15-20 minutes**