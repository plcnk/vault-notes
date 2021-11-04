# Vault-Notes

Notes on how to use Hashicorp Vault

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
