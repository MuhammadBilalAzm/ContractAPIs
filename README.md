# Contract APIs - Automated Testing with CI/CD

Automated Postman API testing for Contract APIs using Newman and GitHub Actions.

## 🚀 Features

- ✅ Automated API testing on push and pull requests
- 📊 HTML test reports with detailed results
- 🔐 Secure handling of API keys using GitHub Secrets
- 🔄 CI/CD integration with GitHub Actions

## 📋 Prerequisites

- Node.js (v20 or higher)
- npm
- GitHub account with repository access

## 🛠️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/MuhammadBilalAzm/ContractAPIs.git
cd ContractAPIs
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment & Credentials

#### Local Development

Update credentials in **`DigitalContracts-dev.postman_environment.json`**:

- **Lines 18-22**: `X-Contracts-ClientId` - Your dev environment client ID
- **Lines 24-28**: `X-Contracts-APIKey` - Your dev environment API key  
- **Lines 30-34**: `SecretKey` - Your dev environment secret key

**Important URLs** (already configured):
- **baseUrl**: `https://api-dev.contracts.com.sa` (Line 7)
- **connectionlurl**: `api-dev.contracts.com.sa` (Line 47)

📖 See [CREDENTIALS.md](CREDENTIALS.md) for detailed instructions on updating credentials.

#### GitHub CI/CD

Configure the `POSTMAN_ENVIRONMENT` secret:

**Path:** `Settings > Secrets and variables > Actions > New repository secret`

| Secret Name | Description | Value |
|------------|-------------|-------|
| `POSTMAN_ENVIRONMENT` | Complete environment JSON | Entire content of `DigitalContracts-dev.postman_environment.json` |

**To update:**
1. Go to: https://github.com/MuhammadBilalAzm/ContractAPIs/settings/secrets/actions
2. Click `POSTMAN_ENVIRONMENT` → "Update secret"
3. Paste the complete updated JSON from your environment file
4. Click "Update secret"

> ⚠️ **Important:** Never commit sensitive credentials to your repository!

### 4. Run Tests Locally

```bash
# Run tests with HTML report
npm test

# Run tests with console output only
npm run test:local
```

## 🔄 CI/CD Pipeline

The GitHub Actions workflow automatically runs tests when:

- Code is pushed to `main`, `master`, or `develop` branches
- Pull requests are created targeting these branches
- Manually triggered via GitHub Actions UI

### Workflow Details

- **Runner:** Ubuntu Latest
- **Node Version:** 20
- **Test Reports:** Uploaded as artifacts (retained for 30 days)
- **Report Location:** Download from Actions > Workflow Run > Artifacts

## 📊 Viewing Test Reports

### In GitHub Actions:

1. Go to **Actions** tab in your repository
2. Click on the latest workflow run
3. Scroll down to **Artifacts** section
4. Download `postman-test-report`
5. Open `report.html` in your browser

### Locally:

After running `npm test`, open `reports/report.html` in your browser.

## 📁 Project Structure

```
ContractAPIs/
├── .github/
│   └── workflows/
│       └── postman-tests.yml       # GitHub Actions workflow
├── My Collection.postman_collection.json  # Postman collection
├── DigitalContracts-dev.postman_environment.json  # Environment file
├── package.json                    # npm dependencies
├── .gitignore                      # Git ignore rules
└── README.md                       # This file
```

## 🔍 Collection Details

- **Collection Name:** My Collection
- **Environment:** DigitalContracts-dev (QA)
- **Tests Include:**
  - Upload Contract (POST)
  - Response validation
  - Status code checks
  - Dynamic contract number generation

## 🛡️ Security Notes

- API keys and secrets are stored in GitHub Secrets
- Environment file in repo contains placeholder values
- Actual values are injected during CI/CD execution
- Reports don't expose sensitive data

## 🤝 Contributing

1. Create a feature branch
2. Make your changes
3. Push to the branch
4. Create a Pull Request
5. Wait for automated tests to pass

## 📝 Scripts

| Command | Description |
|---------|-------------|
| `npm test` | Run tests with HTML report generation |
| `npm run test:local` | Run tests with console output only |

## 🐛 Troubleshooting

### Tests failing locally?

- Ensure environment variables in `DigitalContracts-dev.postman_environment.json` are correct
- Check that Newman is installed: `npm list newman`
- Verify API endpoints are accessible

### GitHub Actions failing?

- Verify all secrets are configured correctly
- Check workflow logs in Actions tab
- Ensure branches match trigger conditions

## 📞 Support

For issues or questions, please open an issue in the repository.

---

**Last Updated:** January 2, 2026  
**Maintained by:** Muhammad Bilal
