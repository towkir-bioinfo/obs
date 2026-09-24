```shell
Restart-Service -Name "CloudflareWARP" -Force
& "C:\Program Files\Cloudflare\Cloudflare WARP\warp-cli.exe" registration delete
& "C:\Program Files\Cloudflare\Cloudflare WARP\warp-cli.exe" connect
```
