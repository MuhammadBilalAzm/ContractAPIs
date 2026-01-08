# API Credentials Configuration

## 🔐 Where to Update Credentials

All API credentials are stored in the environment file:
**`DigitalContracts-dev.postman_environment.json`**

### Required Credentials (Lines 18-32)

Update these three values with your **dev environment** credentials:

1. **X-Contracts-ClientId** (Line 18-22)
   ```json
   {
     "key": "X-Contracts-ClientId",
     "value": "YOUR_CLIENT_ID_HERE",
     "type": "default",
     "enabled": true
   }
   ```

2. **X-Contracts-APIKey** (Line 24-28)
   ```json
   {
     "key": "X-Contracts-APIKey",
     "value": "YOUR_API_KEY_HERE",
     "type": "default",
     "enabled": true
   }
   ```

3. **SecretKey** (Line 30-34)
   ```json
   {
     "key": "SecretKey",
     "value": "YOUR_SECRET_KEY_HERE",
     "type": "default",
     "enabled": true
   }
   ```

## ⚠️ Current Issue

The current credentials may be from a different environment (QA/Production) and are causing:
- **Error E0022**: "Company does not exist" in dev environment

## ✅ What's Already Fixed

- **Host Configuration**: Updated to `api-dev.contracts.com.sa`
- **Signature Calculation**: Now working correctly (no more E0206 "Invalid Signature" errors)
- **SSL Certificates**: Using `--insecure` flag to handle certificate mismatch

## 🔄 How to Update

1. **Get valid dev environment credentials** from your API provider
2. **Edit** `DigitalContracts-dev.postman_environment.json`
3. **Replace** the three credential values (keep them base64 encoded if that's the format)
4. **Test locally**:
   ```bash
   npm test:local
   ```
5. **Update GitHub Secrets** (for CI/CD):
   - Go to: https://github.com/MuhammadBilalAzm/ContractAPIs/settings/secrets/actions
   - Update the `POSTMAN_ENVIRONMENT` secret with the new environment JSON

## 📋 GitHub Secrets Configuration

The CI/CD workflow uses GitHub Secrets to inject credentials at runtime:

- **Secret Name**: `POSTMAN_ENVIRONMENT`
- **Format**: Complete JSON content of `DigitalContracts-dev.postman_environment.json`
- **Location**: Repository Settings → Secrets and variables → Actions

### To Update GitHub Secret:

1. Go to: https://github.com/MuhammadBilalAzm/ContractAPIs/settings/secrets/actions
2. Click on `POSTMAN_ENVIRONMENT`
3. Click "Update secret"
4. Paste the **entire** updated `DigitalContracts-dev.postman_environment.json` file content
5. Click "Update secret"

## 🧪 Testing

After updating credentials, test with:

```bash
# Test with 3 UploadContract APIs
npm test:local

# Full collection test
newman run "My Collection.postman_collection.json" -e "DigitalContracts-dev.postman_environment.json" --insecure --delay-request 1000
```

Expected result: HTTP 200 responses with `"succeeded": true`
