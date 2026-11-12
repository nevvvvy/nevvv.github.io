# SEVHOST License Portal

A responsive, single-page browser portal for checking a hardware ID (HWID) against an externally hosted license list. The current project is a self-contained HTML page using CSS and vanilla JavaScript.

## Live website

https://kirbyjake986-blip.github.io/nevvv.github.io/

GitHub Pages must be configured to deploy the `main` branch from the repository root for this address to serve the latest `index.html`.

## Features

- HWID sign-in and license-list lookup
- HWID helper tools: CMD command, downloadable `SEVHOST_HWID_Finder.bat`, and clipboard support
- Registered-client, HWID, and expiry/status display after a successful check
- Expired and unregistered license feedback
- Browser-side saved HWID convenience and logout
- Responsive dark-themed interface
- Discord community/support and external showcase/download resources

## Project structure

```text
.
└── index.html    # Markup, styles, and JavaScript for the portal
```

No build step, package manager, or separate asset directory is required for the current page.

## How license verification works

1. On page load, the browser requests the text license list from the URL assigned to `GITHUB_URL` in `index.html`.
2. If the direct request fails, the page tries the configured CORS proxy services.
3. `parseHWIDDatabase()` extracts numeric HWIDs and the associated `name` and `date` values.
4. When a visitor submits an HWID, the page looks for a matching record and checks whether its expiry date has passed.
5. A valid record opens the client dashboard; missing or expired records show an error.

The license database must use the format expected by `parseHWIDDatabase()`. Check that function before changing the source data structure.

## External links in the current page

- Discord invite: https://discord.gg/Hs3vYavRW
- Showcase: https://imgur.com/a/Wegueun
- External download: [ID-Gate.exe](https://dl.dropbox.com/scl/fi/sw3eyvj7upr6kz2i5f32d/ID-Gate.exe?rlkey=dod0owyj3yaj8ofztdglphc57&st=o08vrvbs&dl=1)

These destinations are embedded in `index.html` and may change. Verify external files before downloading or distributing them.

## Configuration and editing

### License database

Update the `GITHUB_URL` constant in `index.html` to the raw-text URL of the license list. Keep the file's entries compatible with `parseHWIDDatabase()`.

### Community and resource links

Edit the relevant anchor `href` values in `index.html` when changing Discord, showcase, or download destinations.

### Publish with GitHub Pages

1. Open the repository's **Settings → Pages**.
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Select branch `main` and folder `/(root)`.
4. Save. GitHub Pages will publish the root `index.html` and redeploy after commits to that branch.

## Security and privacy considerations

- **Browser-side HWID checks are not secure authorization.** Visitors can inspect and modify JavaScript running in their own browsers. Do not rely on this page alone to protect paid software or valuable resources.
- **A public license-list URL exposes its contents.** Do not put passwords, API keys, private customer data, or other secrets in this repository or a public text file.
- **Expiry checking is limited by the current implementation.** The page parses month and day and does not enforce a complete year-aware timestamp. Do not rely on it for strict expiry enforcement without improving the date logic.
- **CORS proxies are third-party services.** Proxy requests can disclose the requested database URL and request metadata to those providers. A trusted server-side API is preferable for production authentication.
- **Review downloaded scripts and executables.** The HWID helper is downloaded as a batch file, and the page also links to an external executable. Visitors should verify files and understand them before running them.
- Keep all external links current and confirm that the linked destinations are trustworthy.

## Development

Edit `index.html`, commit the changes to `main`, and allow GitHub Pages to redeploy. Test the page locally and verify the published site after deployment.

For production deployment, move license verification to a server-side service with authentication, access controls, secure data storage, logging, and year-aware expiry validation.
