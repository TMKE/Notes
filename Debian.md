# Debian

### Select default display manager

```bash
sudo dpkg-reconfigure <dm>
```

### sddm display manager

Move the downloaded theme to `/usr/share/sddm/themes/`.

Edit `/etc/sddm.conf` `[Theme]` section.

Use `sddm --example-config` to create a default `sddm.conf` file if the latter doesn't exist.

To preview your changes from your running desktop environment session without logging out: `sddm‑greeter ‑‑test‑mode ‑‑theme /usr/share/sddm/themes/sugar‑candy`.

### Change plymouth theme

Copy the theme folder to `/usr/share/plymouth/themes/YOURTHEME`

Execute:

```bash
sudo plymouth-set-default-theme YOURTHEME -R
```