# SEVHOST License Portal

A responsive, single-page HWID license portal with a dark interface and Filipino-language guidance. The site is built as a self-contained HTML file with embedded CSS and vanilla JavaScript.

## Live website

https://kirbyjake986-blip.github.io/nevvv.github.io/

The URL is served by GitHub Pages when the repository is configured to deploy the `main` branch from the root folder.

## Current interface and features

- **Filipino-language login guidance:** explains how to retrieve and submit the computer's system HWID.
- **System HWID Finder panel:** displays the detected/copied HWID and provides a copy action.
- **CMD helper:** copies a Windows Run command intended to calculate a numeric volume-serial-based HWID and copy it to the clipboard.
- **Batch-file helper:** generates and downloads `SEVHOST_HWID_Finder.bat` for local HWID retrieval.
- **Paste and clipboard support:** lets users paste an HWID into the login field and copy the displayed value.
- **Live license feedback:** checks the entered HWID against the configured database and displays registered, unregistered, expired, or loading states.
- **Client dashboard:** displays the client name, HWID, license expiry text, and an active or lifetime status badge.
- **Session convenience:** saves the last HWID in browser `localStorage`; logout clears the saved value.
- **Showcase and resource links:** includes a Discord invite, Imgur showcase link, and external loader download.
- **Responsive styling:** dark theme with cyan/blue accents, cards, and mobile-friendly layout.

## Project structure

```text
.
└── index.html    # Page markup, styles, and all browser-side JavaScript
```

The current project has no build step, package manager, or separate CSS/JavaScript files.

## License verification flow

1. On page load, the browser requests the license list from the `GITHUB_URL` constant in `index.html`.
2. If the direct request fails, it attempts the configured AllOrigins and corsproxy.io proxy URLs.
3. `parseHWIDDatabase()` parses numeric HWID entries and reads the associated `name` and `date` values.
4. The submitted HWID is compared with the parsed records.
5. Expired or unknown HWIDs are rejected; a matching active record opens the dashboard.

The license database is currently configured as:

```text
https://raw.githubusercontent.com/kupx505/webites/refs/heads/main/Ctool.txt
```

Keep the database syntax compatible with `parseHWIDDatabase()` in `index.html`. Each record is expected to contain a numeric HWID followed by a block with `name` and `date` fields.

## Current external resources

- **Discord community/support:** https://discord.gg/V5pduTcsJV
- **Full showcase:** https://imgur.com/a/Wegueun
- **External loader:** [ID-Gate.exe](https://dl.dropbox.com/scl/fi/sw3eyvj7upr6kz2i5f32d/ID-Gate.exe?rlkey=dod0owyj3yaj8ofztdglphc57&st=o08vrvbs&dl=1)

The video preview element is present in the dashboard. Its source is currently empty in the HTML, so add a valid MP4 source if you want the preview to play a video.

## Configuration and publishing

### Change the license database

Edit the `GITHUB_URL` constant in `index.html` and point it to the raw-text database. Preserve the record structure expected by the parser.

### Change external links

Update the Discord, showcase, and loader anchor URLs in `index.html` when destinations change. Review external downloads before distributing them.

### GitHub Pages

1. Open the repository's **Settings → Pages**.
2. Select **Deploy from a branch** under Build and deployment.
3. Choose branch `main` and folder `/(root)`.
4. Save. GitHub Pages will deploy the root `index.html` after the commit.

## Security and implementation notes

- **Client-side checks are not secure authorization.** Visitors can inspect and modify browser JavaScript. A client-side HWID check should not be the only protection for paid software or sensitive resources.
- **The license database is public.** Anyone who can access its raw URL may be able to read its entries. Do not place passwords, API keys, or private customer information in it.
- **Expiry parsing is not year-aware.** The current `isExpired()` logic compares only month and day (apart from lifetime/no-expiry text). It does not validate a complete date including year; improve this before relying on it for strict license enforcement.
- **The HWID helper uses Windows volume serial information.** This is not a guaranteed unique or tamper-resistant hardware identity and may change with system/storage configuration.
- **CORS proxies are third-party services.** Requests routed through them disclose the requested database URL and request metadata to those providers. A trusted server-side API is preferable for production.
- **Downloaded scripts and executables require review.** Users should inspect helper scripts and verify external downloads before running them.
- **Clipboard access may require a secure context** (such as HTTPS) and browser permission.

## Development

Edit `index.html`, commit the updated file to `main`, and allow GitHub Pages to redeploy. Test changes in a browser and verify the published site after deployment.

For production use, move license verification to a server-side service with authentication, access controls, secure storage, logging, and full year-aware expiry validation.
