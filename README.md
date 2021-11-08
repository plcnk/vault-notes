# Vault-Notes

Notes on how to use Hashicorp Vault.

![Vault Logo](https://www.almtoolbox.com/blog_he/wp-content/uploads/2020/12/hashicorp-vault-logo-1.jpg)

## Install Vault

Add the HashiCorp GPG Key.

```shell
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
```

Add the official HashiCorp Linux repository.

```shell
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
```

Update and install.

```shell
sudo apt update && sudo apt install vault
```

Verify the installation.

```shell
vault version
```

## Start Server

To start the server, run this command:

```shell
vault server -dev
```

Get the vault address and root token and export them into a terminal to use the dev server.

```shell
export VAULT_ADDR='http://127.0.0.1:8200'
export VAULT_TOKEN="your_token"
```

Verify the server is running.

```shell
vault status
```

Note: Don't use dev server in production. Not secure.

## Basic Secrets

By default in a dev server, Key/Value v2 secrets engine is enabled at secret/ path.

The difference between Key/Value v1 and v2 is that version 2 provides versioning and version 1 does not.

### Secrets Usage

Create a secret:

```shell
vault kv put secret/hello foo=world
```

Note: Using multiple commands using different keys will not stack. So your new command will overwrite your previous command. To insert multiple keys, execute this command:

```shell
vault kv put secret/hello foo=world excited=yes
```

Get a secret:

```shell
vault kv get secret/hello
```

Get a certain field:

```shell
vault kv get -field=excited secret/hello
```

Get a certain version:

```shell
vault kv get -version=1 secret/hello
```

List existing keys:

```shell
vault kv list secret/
```

Delete a secret:

```shell
vault kv delete secret/hello
```

Note: Only deletes the latest version. To delete specific versions, execute this command:

```shell
vault kv delete -versions=1,2 secret/hello
```

## Secrets Engines

Secrets Engines are Vault components which store, generate or encrypt secrets. Documentation on various Seccrets Engines available [here](https://www.vaultproject.io/docs/secrets).

### Secrets Engines Usage

Enable a Secrets Engine:

```shell
vault secrets enable kv
```

```shell
vault secrets enable -path=kv kv
```

Note: Path defaults to the name of the Secrets Engine.

List enabled Secrets Engines:

```shell
vault secrets list
```

Disable Secrets Engine:

```shell
vault secrets disable kv/
```
