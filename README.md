# Warning: This action as been deprecated

We recommend using the [crazy-max/ghaction-import-gpg](https://github.com/crazy-max/ghaction-import-gpg) upstream action that this was based on.

# ghaction-import-gpg
GitHub action to import GPG private key

**Note [7/14/22]:** This action has been deprecated in favor of the upstream which now supports sign-only keys, and is well supported and documented.

**Note [5/6/2021]:** This was supposed to be a fork ([paultyng/ghaction-import-gpg](https://github.com/paultyng/ghaction-import-gpg)) of a fork ([crazy-max/ghaction-import-gpg](https://github.com/crazy-max/ghaction-import-gpg)) of the upstream repo. Due to the restrictions on using a sign-only key, we encountered this [issue](https://github.com/crazy-max/ghaction-import-gpg/issues/58). This is an internal action that overrides this fork until the issue is resolved upstream.
## Environment Variables

Following environment variables must be used as `step.env` keys

| Name               | Description                           |
|--------------------|---------------------------------------|
| `GPG_PRIVATE_KEY`  | GPG private key exported as an ASCII armored version (**required**) |
| `PASSPHRASE`       | Passphrase of the `GPG_PRIVATE_KEY` key if set |

Details on how to generate the Private Key and Passphrase can be found in our [learn guide](https://learn.hashicorp.com/tutorials/terraform/provider-release-publish?in=terraform/providers#generate-gpg-signing-key).

## Workflow Example

```yaml
name: sign
on: push

jobs:
  goreleaser:
    runs-on: ubuntu-latest
    steps:
      - name: Import GPG key
        id: import_gpg
        uses: hashicorp/ghaction-import-gpg@v2.1.0
        env:
          GPG_PRIVATE_KEY: ${{ secrets.GPG_PRIVATE_KEY }}
          PASSPHRASE: ${{ secrets.GPG_PASSPHRASE }}
      - run: |
          touch foo.txt
          gpg --detach-sig foo.txt
```
