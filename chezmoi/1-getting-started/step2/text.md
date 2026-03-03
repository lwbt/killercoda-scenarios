# Step 2

## Clone the repo and use the tools

```bash
curl https://mise.run | sh
```{{exec}}

```bash
eval "$(${HOME}/.local/bin/mise activate bash)"
```{{exec}}

```bash
mise install
```{{exec}}

## Verify

And to complete this step just create the file `/tmp/step2`:

```
touch /tmp/step2
```{{exec}}
