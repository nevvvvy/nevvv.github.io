# SEVHOST License Portal

A responsive, single-page browser portal for checking a registered hardware ID (HWID) against an externally hosted license list. The interface is built with HTML, CSS, and vanilla JavaScript; it does not require a build system or package installation.

## Live website

GitHub Pages URL:

https://kirbyjake986-blip.github.io/nevvv.github.io/

The page is served from `index.html` on the `main` branch when GitHub Pages is configured to deploy from the repository root.

## Current features

- **HWID sign-in:** checks the entered HWID against the configured license database.
- **HWID helper:** offers a CMD one-line command and a downloadable `SEVHOST_HWID_Finder.bat` helper, plus clipboard support.
- **License feedback:** displays whether an HWID is registered and whether its license is active or expired.
- **Client dashboard:** shows the registered client name, HWID, and license expiry/status after a successful check.
- **Session convenience:** remembers the last entered HWID in browser `localStorage` and provides a logout action.
- **Community and resources:** includes Discord links, a showcase link, and an external download link.
- **Responsive dark UI:** designed for desktop and mobile screens.

## Project structure

```text
.
└── index.html    # Complete page markup, styles, and JavaScript
```

There is no separate CSS, JavaScript, or build output directory in the current project.

## How the license check works

1. When the page loads, JavaScript requests the text license list from the URL configured in the `GITHUB_URL` constant in `index.html`.
2. If the direct request fails, the page attempts to retrieve the list through configured CORS proxy services.
3. The page parses HWID entries and their associated client name and expiry date.
4. When a visitor submits an HWID, the page checks for a matching entry and evaluates its expiry date.
5. A successful check opens the client dashboard; an unregistered or expired entry displays an error message.

The database text must follow the entry format expected by `parseHWIDDatabase()` in `index.html`, including a numeric HWID and a block containing `name` and `date` values. Review that parser before changing the database format.

## Configuration

### License database

Change the `GITHUB_URL` constant in `index.html` to the publicly reachable raw-text URL of the license list you intend to use. Keep the database format compatible with `parseHWIDDatabase()`.

### Links and downloads

The Discord, showcase, and external download destinations are set in the page markup. Update those links in `index.html` when the destinations change. Verify third-party files and destinations before sharing them with visitors.

## Publish or update with GitHub Pages

1. Open the repository on GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Choose branch `main` and folder `/(root)`.
5. Save. GitHub Pages will publish the root `index.html` and redeploy after later commits.

## Security and privacy notes

- **Client-side validation is not secure authorization.** The license list URL, parsing logic, and browser code are visible to visitors and can be inspected or modified. Do not rely on this page alone to protect paid software or other valuable resources.
- **A public license list exposes its contents.** Do not store private customer information, credentials, API keys, or secrets in a public repository or public text file.
- **Expiry validation is limited.** The current page's date parser compares month and day and does not enforce a complete year-aware timestamp. Review the implementation before relying on it for strict expiry enforcement.
- **CORS proxies are third-party services.** Requests routed through them may expose the requested database URL and request metadata to those services. Prefer a trusted server-side API for production authentication.
- **Downloaded helper scripts run on the visitor's computer.** Explain what the helper does, inspect changes before distributing it, and encourage users to review files before running them.
- **External links can change.** Check download destinations and community links periodically.

## Development

To edit the portal, modify `index.html` and commit the change to `main`. Open the file locally in a browser for a basic preview, then verify the published GitHub Pages site after deployment.

For production use, consider moving license verification to a server-side endpoint with proper authentication, access controls, logging, and year-aware expiry checks.
