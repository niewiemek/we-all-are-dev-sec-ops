# Securly storing credentials

## Environment setup

### GPG instalation
1. Install GPG. Installation guideline can be found [here](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)
1. Use `gpg --full-generate-key` to generate a key.
1. List GnuPG keys with `gpg -k`

### Sops
Install Sops. Installation guideline can ber found [here](https://github.com/mozilla/sops)

### Docker
As an alternative `Dockerfile` can be used for GPG and Sops.
1. Build provided docker file `docker build -t iteratec.io/credentials .`
1. Run docker and attach to it `docker run -it iteratec.io/credentials`

## Encrypting credentials

###
1. Add your public key to .sops.yaml
```
creation_rules:
  - pgp: >-
      C24900C8ACEE5553F168301FCDF899A6F6F56B02,
      --MY_NEW_KEY--
```
1. Encrypt example file with `sops -e config.yaml > config.secure.yaml`
2. Decrypt example file with `sops -d config.secure.yaml`
