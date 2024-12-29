# Deno

Homepage
: [deno.land](https://deno.land)

{type="wide"}

<tabs>
<tab title="Linux &amp; macOS">

```Console
curl -fsSL https://deno.land/install.sh | sh
```

</tab>
<tab title="Windows">

```Console
irm https://deno.land/install.ps1 | iex
```

</tab>
<tab title="Docker">

Docker

```Console
docker pull hayd/alpine-deno:<version>
```

</tab>
</tabs>

## Get the latest version in terminal

```bash
curl -s https://api.github.com/repos/denoland/deno/releases/latest | jq -r '.tag_name' | sed 's/v//'
```
