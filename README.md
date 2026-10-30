# NiX OS updates

Every installed NiX OS computer checks this repository's **latest release** 2 minutes after
login and every 3 hours. When the release's version is newer than the computer's, it shows
"NiX OS X is available" with an **Update now** button.

By Fortifind.org | Henix Cybersecurity Team | Henix Dev Team.

## What a release needs

- **Tag:** the version with a `v` in front, e.g. `v1.2.0` (it must be higher than the last one).
- **Two files attached:** `nix-update.tar.zst` and `nix-update.tar.zst.sha256`.
- **Notes:** the first line is what the popup on every computer shows.

## Making one

On the build PC (the NiX source is in `F:\OSDev\nix-linux`):

```
wsl -d nix-build -- bash /mnt/f/OSDev/nix-linux/tools/make-update.sh 1.2.0
gh release create v1.2.0 F:\OSDev\nix-linux\out\update-1.2.0\nix-update.tar.zst F:\OSDev\nix-linux\out\update-1.2.0\nix-update.tar.zst.sha256 --repo Fortifind-Company/nix-updates --title "NiX OS 1.2.0" --notes "What's new in one line"
```

The update carries the files FortiFind manages (see `protected.list` in the NiX source). To
run commands on every computer once after updating (e.g. install a new package), put them in
`F:\OSDev\nix-linux\update-steps.sh` before making the update.

The repository has to be **public**: computers download releases without signing in to GitHub.
