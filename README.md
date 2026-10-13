# TWX Site Photo Map

A single-page web app for building photo-location slideshows for the weekly PM meeting.

- `index.html` is the whole app. There is nothing to install or build.
- Photos, maps and jobs are stored **in each person's own browser** (not in this repository), so no job data or photos are ever uploaded here.
- Do not commit photos or exported slideshow files to this repository.

## Run it
Open the GitHub Pages address for this repo (Settings -> Pages shows it), for example
`https://YOUR-USERNAME.github.io/YOUR-REPO/photo-map/`

On iPad/iPhone: open it in Safari, tap Share -> Add to Home Screen, and launch it from there for a full-screen app with no browser bars.

## Move jobs between devices (Backup / Restore)
- **Back up**: on the home page (everything), a PM's page (that PM), or a meeting page (that meeting). It saves one `.twxbackup` file with the photos inside.
- **Restore a backup**: on the home page of the other device. It merges: each job keeps whichever copy was edited last, and nothing else on that device is touched.
- Move the file with Google Drive, OneDrive, or AirDrop (backups with photos are usually too big for email).
- PMs can send backups to each other. A PM with the same name, or a meeting on the same date, is merged, not duplicated.

