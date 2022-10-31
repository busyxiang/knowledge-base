# EAS Update
## Environment Variables
It is important to **clear cached environment variables** before you deploy a new over the air (OTA) updates, or else the updates will be using **wrong** environment variables. [GitHub Issue](https://github.com/expo/eas-cli/issues/1123)

```bash
// to clear any cached environment variables
expo export --experimental-bundle --clear

// to rebuild the javascript transform cache
expo r -c

// ...eas command to deploy OTA updates
```
> Once OTA update is **published** and the user **installed** the update, it is **impossible** to revert back to the build version