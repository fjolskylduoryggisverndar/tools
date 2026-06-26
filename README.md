# tools

Parser binaries that do the heavy lifting for the [`rules`](https://github.com/fjolskylduoryggisverndar/rules) repo.

Each tool downloads the latest upstream [Loyalsoldier](https://github.com/Loyalsoldier) data, parses it
(v2ray `geosite.dat` protobuf / MaxMind `Country.mmdb`), and emits sing-box rule-sets per code:

- `sing-geosite` &rarr; `rule-set/geosite-<code>.srs` + `.json` (and `geosite.db` / `geosite-cn.db`)
- `sing-geoip` &rarr; `rule-set/geoip-<code>.srs` + `.json` (and `geoip.db` / `geoip-cn.db`)

These are written relative to the current working directory.

## Releases

Pushing to `master` (or running the workflow manually) builds both tools for `linux/amd64` and publishes
them as assets on a single rolling `latest` release:

- `sing-geosite-linux-amd64`
- `sing-geoip-linux-amd64`

The `rules` repo CI downloads these binaries from
`https://github.com/fjolskylduoryggisverndar/tools/releases/latest/download/<asset>` and runs them.

## Build locally

```bash
cd sing-geosite && go run -v .   # or: go build .
cd sing-geoip   && go run -v .
```

Set `NO_SKIP=true` to force generation regardless of upstream-vs-destination release comparison.
Format with `go generate` (gofumpt + `gofmt -s` + gci).
