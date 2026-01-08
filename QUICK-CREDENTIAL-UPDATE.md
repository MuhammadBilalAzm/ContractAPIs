# 🔐 Quick Credential Update Guide

## Where to Update Your Dev Environment Credentials

### File Location
**`DigitalContracts-dev.postman_environment.json`**

---

## 📝 Step-by-Step Instructions

### 1. Open the Environment File
Open `DigitalContracts-dev.postman_environment.json` in any text editor.

### 2. Update These 3 Values

#### ✏️ Line 20: X-Contracts-ClientId
```json
{
  "key": "X-Contracts-ClientId",
  "value": "YOUR_DEV_CLIENT_ID_HERE",  ← REPLACE THIS
  "type": "default",
  "enabled": true
}
```

#### ✏️ Line 26: X-Contracts-APIKey  
```json
{
  "key": "X-Contracts-APIKey",
  "value": "YOUR_DEV_API_KEY_HERE",  ← REPLACE THIS
  "type": "default",
  "enabled": true
}
```

#### ✏️ Line 32: SecretKey
```json
{
  "key": "SecretKey",
  "value": "YOUR_DEV_SECRET_KEY_HERE",  ← REPLACE THIS
  "type": "default",
  "enabled": true
}
```

### 3. Save the File

### 4. Test Locally
```bash
npm test:local
```

Expected result: HTTP 200 responses with `"succeeded": true`

---

## 🌐 Update GitHub Secret for CI/CD

After updating the local file:

1. **Go to GitHub Secrets**: https://github.com/MuhammadBilalAzm/ContractAPIs/settings/secrets/actions

2. **Click** on `POSTMAN_ENVIRONMENT` secret (or create new if it doesn't exist)

3. **Update the value** with the **ENTIRE** content of your updated `DigitalContracts-dev.postman_environment.json` file:
   - Copy all content from `{` to `}`
   - Paste into the secret value field
   - Click "Update secret"

---

## ✅ What's Already Fixed

You don't need to change these - they're already configured correctly:

- ✅ **baseUrl**: `https://api-dev.contracts.com.sa`
- ✅ **connectionlurl**: `api-dev.contracts.com.sa`
- ✅ **Signature calculation**: Working correctly
- ✅ **SSL handling**: Using `--insecure` flag

---

## ❓ Where to Get Valid Credentials

Contact your API provider to get **dev environment** credentials for:
- `api-dev.contracts.com.sa`

The current credentials may be from QA/Production environment and don't work with the dev API server.

---

## 🐛 Current Error

- **Error Code**: E0022
- **Message**: "Company does not exist"
- **Cause**: Invalid/outdated credentials for dev environment
- **Fix**: Update the 3 credential values above with valid dev credentials
