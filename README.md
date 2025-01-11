# tOS &nbsp; [![bluebuild build badge](https://github.com/thedeveloperever/tos/actions/workflows/build.yml/badge.svg)](https://github.com/thedeveloperever/tos/actions/workflows/build.yml)

This is a Blue-OS Fedora Kionite image with a few modifications for gaming

- Removed Applications
  - Remove Firefox and Thunderbird
  - Remove Plasma Welcome
  - Remove Warehouse for Flatpak

- Added Applications
  - Brave Browser
  - Vesktop
  - Lunar Client

- Changes
  - Install closed source WL driver
    - Personal need for now until I get rid of this Mac
  - Allow hardware debouncing for mice
    - This helps in games that require fast clicking
  - Change OpenGL settings to force disable VSync
    - Achieved with both environment variables and [drirc](https://wiki.archlinux.org/title/Gaming#Reducing_DRI_latency)
  - Use [Arch Linux Latency Parameters](https://wiki.archlinux.org/title/Gaming#Make_the_changes_permanent) for achieving lower input latency
  - Use [Cake Smart Queue Management](https://wiki.archlinux.org/title/Gaming#Reduce_buffer_bloat_on_the_network)
  - Use [Optimized TCP Keep Alive and Recieve Window parameters](https://wiki.archlinux.org/title/Sysctl#Networking)

## Installation

To rebase an existing Fedora Kinoite/Aurora Linux (both are tested and work fine) installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  sudo rpm-ostree rebase ostree-unverified-registry:ghcr.io/thedeveloperever/tos:latest
  ```
- Reboot to complete the rebase:
  ```
  sudo systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/thedeveloperever/tos:latest
  ```
- Reboot again to complete the installation
  ```
  sudo systemctl reboot
  ```

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```
cosign verify --key cosign.pub ghcr.io/thedeveloperever/tos
```
