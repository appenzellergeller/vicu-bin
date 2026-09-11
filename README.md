# vicu-bin

Proposed AUR package recipe for [Vicu](https://github.com/rendyhd/Vicu).
This package will install the prebuilt upstream AppImage.

This is currently not pushed to aur.archlinux.org since the AUR account
registration is closed at the moment.

## Files

- `PKGBUILD` — the build recipe
- `.SRCINFO` — generated metadata cache. Regenerate
  with `makepkg --printsrcinfo > .SRCINFO` any time `PKGBUILD` changes
- `vicu.desktop` — app launcher entry, installed to
  `/usr/share/applications/`
- `vicu.png` — 512×512 icon, installed to
  `/usr/share/icons/hicolor/512x512/apps/`

---

## Part 1 — Steps for AUR publishing

### One-time setup

1. Register account at [aur.archlinux.org](https://aur.archlinux.org).
2. Add public ssh key to account.

### Set upstream and push (creates the package)

```bash
cd ~/Projects/vicu-bin
git remote add aur ssh://aur@aur.archlinux.org/vicu-bin.git
git push aur main:master # yes they use master not main
```

### Updating the package for a new upstream release

Whenever upstream (`rendyhd/Vicu`) tags a new version:

```bash
cd ~/Projects/vicu-bin
rm -f vicu.AppImage          # drop the stale cached download, see gotcha below
sed -i 's/^pkgver=.*/pkgver=NEW_VERSION/' PKGBUILD
sed -i 's/^pkgrel=.*/pkgrel=1/' PKGBUILD
updpkgsums                   # re-downloads and refreshes all sha256sums
makepkg --printsrcinfo > .SRCINFO
git add -A
git commit -m "Update to NEW_VERSION"
git push aur main:master
```

If you only need to change something in the *packaging* (e.g. add a missing
`depends` entry) without a new upstream version, just bump `pkgrel` instead
of `pkgver`, regenerate `.SRCINFO`, commit, push.

---

## Part 2 — Installing locally

Download / clone this repository and run:

```bash
cd ~/Projects/vicu-bin
makepkg -si
```

- `-s` — install any missing build/runtime dependencies via `pacman`
  first (will prompt for your sudo password)
- `-i` — install the resulting package with `pacman` once the build
  finishes

Before updating to a never version, you must delete the `*.Appimage` file first:

```bash
rm -f vicu.AppImage
```

To uninstall vicu-bin: `sudo pacman -R vicu-bin`
