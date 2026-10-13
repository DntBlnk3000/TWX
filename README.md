# TWX Site Photo Map

A single-page web app for building photo-location slideshows for the weekly PM meeting.

- `index.html` is the whole app. There is nothing to install or build.
- Photos, maps and jobs are saved in each browser first, then synced through the TWX Supabase project when signed in to the team login. Nothing is ever stored in this repository.
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

## Cloud sync (Supabase)
- Tap the **Sign in** button (top right) and sign in with the shared TWX team login. Everything then syncs automatically between every device signed in to it. The dot shows the state: green = synced, amber = syncing, grey = offline.
- The app keeps working with no signal. Changes are saved on the device and sync when it's back online.
- If two devices change the same job, the newest edit wins. Deletes sync too.
- Cloud copies of photos are compressed to save space (the full-size originals stay on the device that added them).
- Setup and password reset use a one-time setup code (ask Micah). **Change team password** in the sync panel signs every other device out.
- Backend: Supabase project `TWX Site Photo Map` (`ztafovkhwhnyctksdelo`): `items` table + `push_items()` (newest edit wins), private `photos` bucket, row-level security that only lets the team login in, and the `team-setup` edge function. The key in `index.html` is the public publishable key; access is enforced by those security rules.

