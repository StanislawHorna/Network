# 🌐 Establish Network Connection to the Site

This GitHub Composite Action connects your GitHub Actions runner to your LAN via **Tailscale**
and installs a root certificate from **HashiCorp Vault** to enable secure internal service communication.

## Inputs

| Name                      | Description                             | Required | Default                  |
| ------------------------- | --------------------------------------- | -------- | ------------------------ |
| `TS_OAUTH_CLIENT_ID`      | TailScale OAuth Client ID               | ✅ Yes   | –                        |
| `TS_OAUTH_SECRET_ID`      | TailScale OAuth Secret ID               | ✅ Yes   | –                        |
| `TS_CONNECTION_TAGS`      | TailScale connection tags               | ❌ No    | `tag:ci`                 |
| `VAULT_ROLE_ID`           | HashiCorp Vault Role ID                 | ✅ Yes   | –                        |
| `VAULT_SECRET_ID`         | HashiCorp Vault Secret ID               | ✅ Yes   | –                        |
| `VAULT_ADDR`              | HashiCorp Vault Address                 | ❌ No    | `http://10.0.10.10:8200` |
| `VAULT_CERT_SECRET_PATH`  | Path to the certificate secret in Vault | ❌ No    | `pki/cert/ca`            |
| `VAULT_CERT_SECRET_FIELD` | Field name of the certificate in Vault  | ❌ No    | `certificate`            |

## 🚀 Usage

```YAML
jobs:
  setup-network:
    runs-on: ubuntu-latest
    steps:
      - name: Establish Internal Network Connection
        uses: StanislawHorna/Network/setup-site-link@main
        with:
          TS_OAUTH_CLIENT_ID: ${{ secrets.TS_OAUTH_CLIENT_ID }}
          TS_OAUTH_SECRET_ID: ${{ secrets.TS_OAUTH_SECRET_ID }}
          TS_CONNECTION_TAGS: "tag:ci"
          VAULT_ROLE_ID: ${{ secrets.VAULT_ROLE_ID }}
          VAULT_SECRET_ID: ${{ secrets.VAULT_SECRET_ID }}
          VAULT_ADDR: "http://vault.example.com:8200"
          VAULT_CERT_SECRET_PATH: "pki/cert/ca"
          VAULT_CERT_SECRET_FIELD: "certificate"
```
