# apt

Personal apt repository hosted on GitHub Pages.

## Usage

```sh
curl -fsSL https://danlipsitt.github.io/apt/KEY.gpg | sudo tee /etc/apt/keyrings/danlipsitt.gpg > /dev/null
echo "deb [signed-by=/etc/apt/keyrings/danlipsitt.gpg] https://danlipsitt.github.io/apt/ ./" | sudo tee /etc/apt/sources.list.d/danlipsitt.list
sudo apt update
```

## Adding a new package

Packages are added via the reusable `publish.yml` workflow. In the source repo's workflow:

```yaml
jobs:
  publish:
    uses: DanLipsitt/apt/.github/workflows/publish.yml@main
    with:
      artifact-name: my-package-deb   # name of the uploaded artifact containing .deb files
      commit-message: "Update my-package to v1.2.3"
    secrets:
      deploy-key: ${{ secrets.APT_DEPLOY_KEY }}
```

The deploy key (`APT_DEPLOY_KEY`) must be an SSH private key with write access to this repo.

To create and register the key:

```sh
# Generate the key pair
ssh-keygen -t ed25519 -C "apt-deploy" -f apt_deploy_key -N ""

# Add the public key as a deploy key in DanLipsitt/apt (Settings → Deploy keys → Add)
cat apt_deploy_key.pub

# Add the private key as a secret in the source repo (Settings → Secrets → Actions → New)
# Secret name: APT_DEPLOY_KEY
cat apt_deploy_key

# Clean up local key files
rm apt_deploy_key apt_deploy_key.pub
```

## Packages

- **camilladsp** — CamillaDSP audio signal processor
- **camillagui** — CamillaGUI web interface for CamillaDSP
