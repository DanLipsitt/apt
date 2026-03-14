# apt

Personal apt repository hosted on GitHub Pages.

## Usage

```sh
curl -fsSL https://danlipsitt.github.io/apt/KEY.gpg | sudo apt-key add -
echo "deb https://danlipsitt.github.io/apt ./" | sudo tee /etc/apt/sources.list.d/danlipsitt.list
sudo apt update
```

## Packages

- **camilladsp** — CamillaDSP audio signal processor
- **camillagui** — CamillaGUI web interface for CamillaDSP
