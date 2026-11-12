# SEVHOST License Portal

A lightweight, responsive, single-page license portal built with HTML, CSS, and vanilla JavaScript.

## Live website

When GitHub Pages is enabled, the site is available at:

https://kirbyjake986-blip.github.io/nevvv.github.io/

## Features

- License sign-in using a submitted hardware ID (HWID)
- HWID helper with copy/paste support
- License status and expiry display
- Discord support links
- Showcase and loader resource links
- Responsive dark interface

## Project structure

```text
.
└── index.html
```

The website is served directly from `index.html`. No build step or package installation is required.

## Publishing with GitHub Pages

1. Open the repository **Settings**.
2. Select **Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select the `main` branch and the `/(root)` folder.
5. Save the settings and wait for the deployment to finish.

## License database configuration

The page currently reads its license list from the external URL configured by the `GITHUB_URL` constant in `index.html`.

To use a different database, update that constant to the correct publicly accessible raw-text URL and make sure its content matches the format expected by the page's parser.

## Important security notes

- This is a browser-side demo/portal. A HWID check performed in JavaScript is not a secure authorization boundary; users can inspect and modify client-side code.
- Do not put private API keys, passwords, secrets, or sensitive customer data in this repository or in browser-delivered code.
- The configured license database URL is visible to visitors. Do not use a public text file as the sole protection for valuable software or private license records.
- Review external download links and make sure visitors understand what they are downloading before distributing them.

## Editing

Edit `index.html` and commit the changes to the `main` branch. GitHub Pages will redeploy the site automatically when configured to deploy from that branch.
