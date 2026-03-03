# Step 2

## Clone the repo and use the tools

```bash
git clone --depth 1 https://github.com/flathub/org.jellyfin.JellyfinServer.git
cd org.jellyfin.JellyfinServer
```{{exec}}

```bash
curl https://mise.run | sh
eval "$(${HOME}/.local/bin/mise activate bash)"
cd; cd -
```{{exec}}

```bash
mise install
mise use -g lazygit
```{{exec}}

```bash
just
```{{exec}}

## TODO: Tooling and data

```bash
mise use -g gum
mise use -g btop
```{{exec}}

```bash
flatpak ps
```{{exec}}

```bash
flatpak info --show-permissions org.jellyfin.JellyfinServer
```{{exec}}

```bash
flatpak info --show-location org.jellyfin.JellyfinServer
```{{exec}}

> **Note:** You need to install `tree`. Use: `sudo apt install -y tree`{{exec}}

```bash
tree $(flatpak info --show-location $(flatpak list --columns=ref | gum choose)) | less
```{{exec}}

```bash
flatpak list
```{{exec}}

## TODO: Rollback to an earlier version

```bash
flatpak remote-info --log flathub org.jellyfin.JellyfinServer
```{{exec}}

```bash
flatpak update \
  --commit=$(flatpak remote-info --log --show-commit flathub org.jellyfin.JellyfinServer | gum choose) \
  org.jellyfin.JellyfinServer
```{{exec}}

## TODO: Security -- Firewall

Since the traffic is sent unencrypted, you should not expose the service outside the host. Therefore we will configure firewall rules with UFW, which ships with Ubuntu. On other systems you would use `firewall-cmd`.

```bash

```{{exec}}

You could use Tailscale to expose the service on your personal Tailnet. Setting up Tailscale is beyond the scope of this tutorial, and it makes more sense setting it up for yourself. The Tailscale YouTube channel is very helpful.

## TODO: Reverse Proxies

- Tailscale
- Cloudflared
- Caddy

## Verify

And to complete this step just create the file `/tmp/step2`:

```
touch /tmp/step2
```{{exec}}
