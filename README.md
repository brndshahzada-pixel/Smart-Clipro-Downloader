# Smart Clipro Downloader — update channel

This public repository is the **update channel** of the Clipro Windows app. It holds GitHub **Releases** and one file, `version.json`. No source code.

Clipro.exe checks, in the background at start, BOTH of these (the higher version wins):

    https://github.com/brndshahzada-pixel/Smart-Clipro-Downloader/releases/latest/download/version.json
    https://raw.githubusercontent.com/brndshahzada-pixel/Smart-Clipro-Downloader/main/version.json

1. the `version.json` asset of the newest **published** release (drafts / pre-releases are not seen);
2. `version.json` in this repo (branch `main`).

Builds made before 2026-11-14 10:30 PKT (the 1.3.0 test build) read only the first one, so every release should carry `version.json` as an asset too.

## Every release

| File | Where | Made by |
|---|---|---|
| `Clipro-vX.Y.Z.zip` | release asset | `BUILD_RELEASE.bat` → `release\Clipro-vX.Y.Z.zip` (exactly Clipro.exe + updater.exe.new) |
| `version.json` | release asset **and** this repo | `BUILD_RELEASE.bat` → `release\version.json` (version, download_url, sha256, size, changelog) |

Release tag = plain version, e.g. `1.3.1`. Download URL: `.../releases/download/X.Y.Z/Clipro-vX.Y.Z.zip`.

Never edit the sha256 or size by hand: the updater refuses a download whose SHA-256 or size does not match.

## Publishing (summary)

1. Build and test on Windows (`BUILD_RELEASE.bat noinstaller` → verify PASS, `tools\dev\TEST_UPDATER.bat` → ALL PASSED).
2. Releases → Draft a new release → tag `X.Y.Z` → upload both files → Save draft.
3. `tools\release_build.py checkrelease X.Y.Z` → PASS. Publish. Commit the same `version.json` here.

Full steps: `docs/UPDATER.md` in the private source repository.
