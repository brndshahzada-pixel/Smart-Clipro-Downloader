# Smart Clipro Downloader — update channel

This public repository is the **update channel** of the Clipro Windows app. It holds only GitHub **Releases**, no source code.

Clipro.exe checks, in the background at start:

    https://github.com/brndshahzada-pixel/Smart-Clipro-Downloader/releases/latest/download/version.json

That is the `version.json` asset of the newest **published** release. Drafts and pre-releases are not seen by users.

## Every release has exactly two assets

| Asset | Made by |
|---|---|
| `Clipro-vX.Y.Z.zip` | `BUILD_RELEASE.bat` → `release\Clipro-vX.Y.Z.zip` (Clipro.exe + updater.exe.new) |
| `version.json` | `BUILD_RELEASE.bat` → `release\version.json` (version, download_url, sha256, size, changelog) |

Upload both files **unchanged**. Never edit the sha256 or size by hand: the updater refuses a download whose SHA-256 does not match.

## Publishing (summary)

1. Build and test on Windows (`BUILD_RELEASE.bat`, then `tools\dev\TEST_UPDATER.bat` → ALL PASSED).
2. Releases → Draft a new release → tag `vX.Y.Z` → upload the two files → **Save draft**.
3. `tools\release_build.py checkrelease vX.Y.Z` (with `GITHUB_TOKEN` set for a draft) → PASS.
4. Publish. Run `checkrelease vX.Y.Z` again → PASS.

Full steps: `docs/UPDATER.md` in the private source repository.
