# TASKS: full/REFIT Launcher

## T01 [COMPLETE] Audit live Vercel account
- Output: 81 live Vercel project records
- Acceptance: paginated `vercel projects ls --json` returns 81 projects

## T02 [COMPLETE] Reconcile Airtable inventory
- Output: 17 missing project rows plus launcher row created in Airtable table `tblH8Ib9amC9uQyaI`
- Acceptance: every live Vercel project ID exists in Airtable, with one pre-existing stale Airtable row retained

## T03 [COMPLETE] Build static PWA launcher
- Output: `/Users/paul/dev-4/fullrefit-launcher/index.html` and supporting catalog, JavaScript, CSS, manifest, and service worker
- Acceptance: local smoke and browser smoke pass with 80 launcher cards and 80 links

## T04 [COMPLETE] Publish GitHub repository
- Output: `https://github.com/fullREFIT/fullrefit-launcher`, branch `main`
- Acceptance: remote repository and latest commit `fd34e61` verified by `gh repo view` and git status

## T05 [COMPLETE] Deploy and verify Vercel production
- Output: `https://fullrefit-launcher.vercel.app`
- Acceptance: production HTTP 200, 80 rendered cards, 80 links, service worker registered, mobile overflow false, zero browser console errors
