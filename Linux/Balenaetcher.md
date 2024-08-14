## 1. Downloading BalenaEtcher

Visit BalenaEtcher [GitHub Latest Release page.](https://github.com/balena-io/etcher/releases/latest)

## 2. Enable the Ubuntu Universe repository

There are a few packages that we require to use the BalenaEtcher and are available through the Universe repository. Therefore use the given command and enable the Repo on your system before following the rest of the steps.

```bash
sudo add-apt-repository universe
```

## 3. Installing BalenaEtcher on Ubuntu 22.0 LTS

```bash
cd Downloads
```

```bash
ls
```

```bash
sudo apt install ./balena-etcher_*_amd64.deb
```

1. If you are about to use the **APPImage** or getting some problems due to **libappindicator1** then don’t forget to install it.

```bash
sudo apt install libappindicator1
```

