# pkg-mate-desktop (Menta Linux)

Debian packaging of mate-desktop 1.29.1 (from debian-mate-team/mate-desktop on
Salsa, 1.28.2-1). Builds: mate-desktop, mate-desktop-common, libmate-desktop-2-17t64,
libmate-desktop-dev, libmate-desktop-doc, gir1.2-matedesktop-2.0.

Versioning: `<upstream>-<debian rev>mentaN`, e.g. `1.29.1-1menta1`; bump with `dch -i`.
Upstream has no Wayland build switch; its Wayland handling is unconditional.

CI builds on every push to `master`; pushing a tag `menta/<version>` also
publishes the .debs as a GitHub release.
