# Description

A Template Vue SPA using Ant Design Vue UI and built with Vite

## Read Me FIRST!

TBD... Instructions on working with templates

## Setup

1. setup to allow incoming merge from upstream template update

```bash
# run once only after
# - clone, or
# - fork, or
# - deleting .git and running git init
./setup-upstream.sh
```

2. setup for your project

# copy the sample environment
```bash
# setup your env file
cp .env.development.sample .env.development

# setup apploader.js to choose folder to use for development in src/apps
cp src/apps/apploader.js.sample src/apps/apploader.js

# to make your custom app you can either
# - 1. continue development in src/apps/web-sample
# - 2. rename src/apps/web-sample and develop from there
# - 3. make a copy of apps/web-sample and rename it and work from there
```

In `src/apps/apploader.js`, change the `web-sample` to the folder you are using for development

```
import setup from './web-sample/setup.js'
```

3. Important notes for development

- change only the package.json in apps/web-sample
- do note any conflicts to resolve for anything outside the apps folder when merging from upstream
- feedback for improvement is welcome

4. Updating the template

```bash
git fetch upstream
git merge upstream/main
```

## Install & Run & E2E Test

```bash
npm install
cd src/apps/<your custom development folder> default is `web-sample`
npm install
cd ../../..
npm run dev # using the dev server
```

3. Visit

- http://127.0.0.1:8080/ to view application

**Note For Login**

Login using one of the following:
  
- Mocked [NOTE: API calls to protected Endpoints WILL FAIL!]:
  - Login: fake a user and login, no backend needed, just click button
  - Login Callback: fake a callback and set fake user and login, no backend needed, just click button
- Login: normal login with OTP, express server needs to be run
  - details already **prefilled** with following values, just click on Login button
  - User: test
  - Password: test
  - OTP (if enabled - e.g. USE_OTP=TEST): use 111111 as otp pin, already prefilled, click on OTP button
- Enterprise SSO (SAML2, OIDC) refer to [https://github.com/ais-one/cookbook]() on sample implementation


4. E2E Testing

```bash
npx playwright install chromium
npx playwright test --browser=chromium

cd src/apps/web-sample
npm run test:e2e
```

## Project Strcuture

```
+- nested/ : testing for multi-html
+- public/
|  +- img/
|  |  +- icons/
|  |  +- splash/
|  +- static/
|  +- favicon.ico
|  +- manifest.json
|  +- robots.txt
|  +- service-worker.js
|  +- sitemap.xml
|  +- style.css
+- src/
|  +- apps/
|  |  +- web-<Your-Custom-Frontend>/: folder with prefix "-web" are your custom frontend code (your frontend repo)
|  |  +- web-sample/
|  |     +- components/
|  |     +- layouts/
|  |     +- tests/
|  |     +  +- example.spec.js
|  |     +- views/
|  |     +- .gitignore: for your repo
|  |     +- hookFns.js
|  |     +- package.json
|  |     +- playwright.config.js
|  |     +- setup.js: custom frontend setup (set INITIAL_SECURE_PATH, ROUTES CONSTANTS here)
|  |     +- store.js: custom frontend store
|  |  +- apploader.js.sample : to create apploader.js from this sample
|  +- layouts/
|  +- mocks/ : for msw later
|  +- plugins/ : i18n, fetch, ws (websocket), useMediaQuery
|  +- views/
|  +- App.vue
|  +- main.js
|  +- pwa-init.js
|  +- router.js
|  +- services.js
|  +- store.js
+- .env.development.sample : to create other envs
+- .eslintignore
+- .eslintrc.js
+- .gitguardian.yml
+- .gitignore
+- .prettierrc.js
+- config.js
+- index.html
+- package.json
+- README.md
+- vite.config.js
```

---

## Frontend Custom Application Notes

Setting up your custom frontend

**Notes:**
- in **package.json**, default environment for `vite` command is `development`
- `.env.<environment>` and `apploader.js` files are specific to each application and found in `src/web<your-web-app>/deploy` folder, **they are copied to root folder** when switching app to work on
- **apploader.js** contains the app setup file to use
- `.env.[MODE]` indicates the environment file to use (command to use: npx vite build --mode $1)
- All folders and files prefixed with TBD can be ignored, they are not implemented and used for reference

```bash
# in src/apps
# note that project name must start with prefix "web-"
git clone <your frontend project e.g. web-example>
```
- see **.env.development** for defining vite.config.js and environment level (eg API URL) related configurations
- see **apploader.js** for loading custom frontend
- environment is selected using the --mode property (see package.json)
- use **src/apps/web-sample/** as reference on your custom frontend
- see **src/apps/web-sample/setup.js** on the frontend setup especially the ROUTES property
- ROUTES property
  - use kebab-case, will be converted to Capital Case in menu display
  - only up to 1 submenu level
    - /first-level
    - /submenu/second-level
  - paths
    - '~/xxx.js' from **<project>/src** folder
    - '/xxx.js' from **<project>** folder


### Sample Deployment - WIP to test

1. configure .env.production
2. run the following workflow `.github\workflows\sample-manual-gh-pages.yml`, select env as production


## Notes & Todos

- [Why Use Vite](https://indepth.dev/a-note-on-vite-a-very-fast-dev-build-tool/)
- Mocks are not ready yet
- Tests are not ready yet

