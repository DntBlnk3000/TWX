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

## Automatic 2-week cleanup
- Each meeting date is deleted, with its jobs, site maps and photos, **14 days after the meeting date** (a 10.6 meeting goes on 10.20). It's deleted on every device and in the cloud. Each meeting card shows its "auto-deletes" date.
- A meeting created after its date (or given a past date by mistake) gets 14 days from the day it was created. Jobs with no meeting date go after 14 days without edits.
- Cleanup never runs while a job is open or a slideshow is showing. To keep something longer, **Back up** the meeting first.
- Deleting a job also removes its photos from the cloud, even on a device that never downloaded them.

## Procore photo exports
- In a job, **+ Add photos** (or drag and drop) accepts a Procore **ZIP** download or a Procore **PDF** photo export, as well as normal photos.
- A ZIP is unzipped in the browser; only image files are added (CSV files and Mac/hidden files are skipped).
- A PDF is split into its embedded photos, in page order, at the size stored in the PDF. Logos or icons that repeat on every page are left out.
- The PDF reader (pdf.js) and, on older phones, an unzip helper (fflate) load from a CDN the first time they're needed, so that step needs an internet connection.

## Cloud sync (Supabase)
- Tap the **Sign in** button (top right) and sign in with the shared TWX team login. Everything then syncs automatically between every device signed in to it. The dot shows the state: green = synced, amber = syncing, grey = offline.
- The app keeps working with no signal. Changes are saved on the device and sync when it's back online.
- If two devices change the same job, the newest edit wins. Deletes sync too.
- Cloud copies of photos are compressed to save space (the full-size originals stay on the device that added them).
- **Photos download per PM.** Every device gets every PM's meeting dates and jobs, but only downloads photos for the PM last opened on that device (opening a PM's page, meeting or job picks that PM). Opening, presenting, exporting or backing up another PM's job downloads its photos first. A job never opens without its photos, so a phone with no signal can't accidentally drop them.
- Setup and password reset use a one-time setup code (ask Micah). **Change team password** in the sync panel signs every other device out.
- Backend: Supabase project `TWX Site Photo Map` (`ztafovkhwhnyctksdelo`): `items` table + `push_items()` (newest edit wins), private `photos` bucket, row-level security that only lets the team login in, and the `team-setup` edge function. The key in `index.html` is the public publishable key; access is enforced by those security rules.

