# esphome
esphome yaml files

## Doorbell & weather wall display project
Client project docs: [PRD.md](doorbell-weather-display/PRD.md) (requirements & architecture), [BOM.md](doorbell-weather-display/BOM.md) (bill of materials), [presence-node.yaml](presence-node.yaml) (mmWave presence sensor firmware).

## Setup

Dependencies are managed with [uv](https://docs.astral.sh/uv/). Install it once:

```
curl -LsSf https://astral.sh/uv/install.sh | sh              # macOS / Linux
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"   # Windows
```

Then, from the repo root:

```
uv sync
```

`uv sync` reads `uv.lock` and installs the exact pinned versions, fetching a
matching Python (see `.python-version`) if you don't already have one. There is
no separate virtualenv step.

Create a `secrets.yaml` in the repo root (it is gitignored) with the keys the
configs reference: `wifi_ssid`, `wifi_password`, `SSID`, `SSID_PASS`, `AP_PASS`,
`hass_password`, `ota_password`, `mqtt_broker`, and `api_encryption_key`.
Generate the API key with `openssl rand -base64 32`.

## Usage

Prefix esphome commands with `uv run`:

```
uv run esphome config dht-only.yaml     # validate
uv run esphome run dht-only.yaml        # build + upload
uv run esphome logs dht-only.yaml       # stream logs
```

## Updating dependencies

```
uv lock --upgrade    # re-resolve to the newest allowed versions
uv sync              # apply them locally
```

Commit the resulting `uv.lock`. Dependabot also opens weekly PRs for this
(see `.github/dependabot.yml`).