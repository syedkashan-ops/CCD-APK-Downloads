# CCD Attendance — free GitHub Pages APK download portal

This is a **static public portal** based on the CCD project's existing `ccd_header.jpg` and app icon. It does not host or process employee attendance data.

## Step 1 — Create a separate PUBLIC distribution repository

On your Android phone, open GitHub → **+** → **New repository**. Name it `CCD-APK-Downloads` and choose **Public**. Do **not** publish the Android source code, Supabase credentials, `.jks` signing key or workflow secrets here. GitHub Pages sites are public, even if the source repository is private on supported plans.

**Important:** Get authorization to publish PSO-branded materials and the APK publicly. A public download link is not employee-only access. If public distribution is not approved, do not deploy this portal; use an approved authenticated internal channel instead.

## Step 2 — Upload portal files

Upload `index.html`, `ccd_header.jpg`, and `ccd_icon.png` to the repository root (GitHub → Add file → Upload files). On mobile Chrome, Desktop site may help.

Edit `index.html`: find `REPLACE_GITHUB_USERNAME/CCD-APK-Downloads` and replace `REPLACE_GITHUB_USERNAME` with your actual GitHub username. Commit the edit.

## Step 3 — Enable GitHub Pages

Repo **Settings → Pages → Build and deployment → Deploy from a branch**. Choose branch `main`, folder `/(root)`, then **Save**. Wait for deployment. Your address will normally be:

`https://YOUR_USERNAME.github.io/CCD-APK-Downloads/`

Do not assume this URL is live until GitHub Pages confirms it.

## Step 4 — Publish the APK (NOT the AAB)

In this **public distribution repository**, open **Releases → Draft a new release**. Use a version tag such as `v2.9` (a normal published release, NOT prerelease). Title: `CCD Attendance v2.9`. Attach the tested APK and ensure its release asset filename is exactly:

`CCD-Attendance.apk`

Publish the release. Reload the portal. It reads GitHub's public latest-release API and enables the download button automatically. For each subsequent version, create a newer published release with the same APK asset filename and a higher version tag.

**APK signing:** A debug APK may be installable for limited testing but is not suitable for a trusted large-scale deployment. Prefer a dedicated signed release APK. For updates to install over existing copies, package name and signing certificate must match, and the version code must increase. Avoid uploading the AAB: users cannot install an AAB directly.

**GitHub release storage:** This uses GitHub Release assets rather than GitHub Actions artifact storage; check applicable GitHub limits and policies. This portal does not fix an APK build failure or automatically move files from your private source repository.

## Test before sharing

1. Open portal on a phone; check images and latest-version label.
2. Tap Download and verify `.apk` is downloaded.
3. Verify package/application identity and signing certificate; test installation on an approved test device.
4. Test IN/OUT, GPS permission, offline queue, sync, and update from an earlier signed build.
5. Obtain employer authorization and a security review before sharing with 1,100 employees.

## Security note

GitHub Pages and a public GitHub Release provide **public** access. Do not treat an unlisted URL as private. Ensure the Android application enforces backend authentication/authorization and Supabase Row Level Security independently of how the APK is distributed. Never put service-role keys or other secrets inside an APK.
