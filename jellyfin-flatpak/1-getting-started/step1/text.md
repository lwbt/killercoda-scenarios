# Step 1

## OS Info

```bash
source /etc/os-release;echo -e "OS:\t${PRETTY_NAME}\nUser:\t$USER (uid: ${UID})\n"
```{{exec}}

```bash
uname -a
uptime
```{{exec}}

```bash
lscpu
```{{exec}}

## Install

```bash
sudo apt install -y flatpak
```{{exec}}

```bash
flatpak remote-add --if-not-exists flathub \
  https://dl.flathub.org/repo/flathub.flatpakrepo
```{{exec}}

Now pick the installation command of your choice **minimal output** or **interactive output**.

Minimal looks like this:

> ```
> Installing runtime/org.freedesktop.Platform.GL.default/x86_64/24.08
> Installing runtime/org.freedesktop.Platform.GL.default/x86_64/24.08extra
> Installing runtime/org.freedesktop.Platform.Locale/x86_64/24.08
> Installing runtime/org.freedesktop.Platform.openh264/x86_64/2.5.1
> Installing runtime/org.freedesktop.Platform/x86_64/24.08
> Installing app/org.jellyfin.JellyfinServer/x86_64/stable
> ```

Minimal ouput install command:

```bash
flatpak install -y --noninteractive flathub org.jellyfin.JellyfinServer
```{{exec}}

Normal output install command:

> **Note:** Some charaters might not display correctly here.

```bash
flatpak install -y flathub org.jellyfin.JellyfinServer
```{{exec}}

## Start the server

```bash
flatpak run --command=jellyfin \
  org.jellyfin.JellyfinServer --service
```{{exec}}

## Launch the Web UI

[Access Jellyfin Web Interface]({{TRAFFIC_HOST1_8096}})

- User: `kc-internal`{{copy}}
- Password: `123456`{{copy}}

## Check data folder

```bash
du -hs .var/app/org.jellyfin.JellyfinServer
ls -l .var/app/org.jellyfin.JellyfinServer
```{{exec}}

## Add media

```bash
mkdir videos
cd videos
wget https://repo.jellyfin.org/test-videos/SDR/AVC/Test%20Jellyfin%201080p%20AVC%203M.mp4
cd
mv -v "videos/Test Jellyfin 1080p AVC 3M.mp4" "Jellyfin Server Media/"
```{{exec}}

```bash
flatpak info --show-permissions org.jellyfin.JellyfinServer
```{{exec}}

```bash
flatpak override --filesystem=~/videos:ro  org.jellyfin.JellyfinServer
```{{exec}}

```bash
flatpak info --show-permissions org.jellyfin.JellyfinServer
```{{exec}}

At *Add Media Library* choose:
- Folder: `/root/Jellyfin Server Media`{{copy}}

## Verify

Please create file `/tmp/step1`:

```
touch /tmp/step1
```{{exec}}
