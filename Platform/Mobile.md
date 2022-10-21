# Deep Linking
## Frontend Setup
In the `public` folder, create `.well-known` folder which need to have `assetlinks.json` for **Android** and `apple-app-site-association` for  **iOS**.

### Android Example
```json
[
  {
    "relation": ["delegate_permission/common.handle_all_urls"],
    "target": {
      "namespace": "android_app",
      "package_name": "com.example.app",
      "sha256_cert_fingerprints": [
        "your_app_fingerprints"
      ]
    }
  }
]
```
>You can get the fingerprint from your **Play Console** app `Setup > App Integrity > App Signing > SHA-256 certificate fingerprint`

### Apple Example
```json
{
  "applinks": {
    "apps": [],
    "details": [
      {
        "appID": "LKWJEF.io.myapp.example",
        "paths": [
          "/*",
          "/records/*"
        ]
      }
    ]
  }
}
```
> The **appID** field uses the following format `<Application Identifier Prefix>.<Bundle Identifier>`

> `Application Identifier Prefix` is your developer account **Team ID**

## Validate
Use the following links to validate the hosted files for [Android](https://digitalassetlinks.googleapis.com/v1/statements:list?source.web.site=https://<domain>&relation=delegate_permission/common.handle_all_urls) and [Apple](https://branch.io/resources/aasa-validator/)