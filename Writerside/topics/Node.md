# Node.JS

Homepage
: [nodejs.org](https://nodejs.org)

{type="wide"}

## Installing Node.js

There are several ways to install Node.js on your system, including using a package manager, downloading the installer from the Node.js website, or using a version manager like `nvm`.

### Package Manager

<tabs>
<tab title="nvm">

nvm (Node Version Manager)

```Console
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash
nvm install <version>
```

</tab>
<tab title="fnm">

fnm (Fast Node Manager)

```Console
curl -fsSL https://fnm.vercel.app/install | bash
source ~/.bashrc
fnm use --install-if-missing <version>
```

</tab>
<tab title="Brew">

Homebrew (macOS)

```Console
brew install node@<version>
```

</tab>
<tab title="Chocolatey">

Chocolatey (Windows)

```Console
choco install nodejs
```

</tab>
<tab title="Docker">

Docker

```Console
docker pull node:<version>-alpine
```

</tab>
</tabs>