## GitHub Pages
 [gh-pages](https://www.npmjs.com/package/gh-pages) is the package to go to deploy the repository to GitHub pages

### Deploy with Command
1. Add script to deploy
```
"scripts": {
  "deploy": "gh-pages -d build"
}
```

2. Deploy
```bash
npm run build
npm run deploy
```

### Vite
In the `vite.config.js` need to set the correct base URL.

If you are deploying to `https://<USERNAME>.github.io/<REPO>/`, for example your repository is at `https://github.com/<USERNAME>/<REPO>`, then set `base` to `'/<REPO>/'`

[SOURCE](https://vitejs.dev/guide/static-deploy.html#github-pages)