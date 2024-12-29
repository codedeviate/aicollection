# Bun

Homepage
: [bun.sh](https://bun.sh)

{type="wide"}

<tabs>
<tab title="Linux &amp; macOS">

```Console
curl -fsSL https://bun.sh/install | bash
```

</tab>
<tab title="Windows">

```Console
powershell -c "irm bun.sh/install.ps1 | iex"
```

</tab>
<tab title="Docker">

Docker

```Console
docker pull jarredsumner/bun:<version>
```

</tab>
</tabs>

## Get the latest version in terminal

```bash
curl -s https://api.github.com/repos/oven-sh/bun/releases/latest | jq -r '.tag_name' | sed 's/bun-v//'
```