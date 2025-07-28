# 🔐 Install Internal Root Certificate

This GitHub Composite Action securely retrieves a **root certificate** from **HashiCorp Vault**
and installs it into the runner’s trust store.
This allows GitHub-hosted runners to trust internal services that use a custom Certificate Authority (CA).

## Inputs

| Name                      | Description                            | Required | Default                  |
| ------------------------- | -------------------------------------- | -------- | ------------------------ |
| `VAULT_ROLE_ID`           | HashiCorp Vault AppRole Role ID        | ✅ Yes   | –                        |
| `VAULT_SECRET_ID`         | HashiCorp Vault AppRole Secret ID      | ✅ Yes   | –                        |
| `VAULT_ADDR`              | Vault address                          | ❌ No    | `http://10.0.10.10:8200` |
| `VAULT_CERT_SECRET_PATH`  | Path to the Vault secret               | ❌ No    | `pki/cert/ca`            |
| `VAULT_CERT_SECRET_FIELD` | Field name of the certificate in Vault | ❌ No    | `certificate`            |

---

## 🚀 Usage

```YAML
jobs:
  trust-internal-ca:
    runs-on: ubuntu-latest
    steps:
      - name: Install Internal Root CA Certificate
        uses: ./install-root-cert
        with:
          VAULT_ROLE_ID: ${{ secrets.VAULT_ROLE_ID }}
          VAULT_SECRET_ID: ${{ secrets.VAULT_SECRET_ID }}
          VAULT_ADDR: "http://vault.example.com:8200"
          VAULT_CERT_SECRET_PATH: "pki/cert/ca"
          VAULT_CERT_SECRET_FIELD: "certificate"
```
