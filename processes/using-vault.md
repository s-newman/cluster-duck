HashiCorp Vault User's Guide
============================

HashiCorp Vault is used by the Operations Program for several tasks, but it can be a bit confusing to get started with. This document will provide an overview of how to perform some of the more common vault operations with the Vault CLI. For a complete guide on using the Vault CLI, please see the official [vault documentation](https://www.vaultproject.io/docs/commands/index.html).

## Installation

Installing Vault is pretty simple. We recommend downloading the precompiled binaries from the official website. Use the following links to install the Vault CLI on your system:

- [download precompiled binary](https://www.vaultproject.io/downloads.html)
- [installation instructions](https://learn.hashicorp.com/vault/getting-started/install)

If you _really_ want to compile the Vault CLI yourself (not recommended), check out the [official documentation](https://www.vaultproject.io/docs/install/index.html) and have fun.

## Logging In

Before you can run any Vault commands, you must log in with your username and password. If you do not have a username and password, bother an admin to give you credentials before continuing.

First, you must export a few environment variables so the Vault CLI knows how to connect to our Vault server. This process differs for PowerShell and Bash/Bash-like terminals.

On pretty much any Mac/Linux/Unix terminal, you can export the environment variables as follows:

```shell
export VAULT_ADDR="https://vault.ritsec.cloud:8200"
export VAULT_SKIP_VERIFY=1
```

In PowerShell, instead run the following commands:

```ps1
$env.VAULT_ADDR = 'https://vault.ritsec.cloud:8200'
$env.VAULT_SKIP_VERIFY = '1'
```

The `VAULT_SKIP_VERIFY` variable is required because (at the time this was written) Vault uses an invalid certificate. You can double-check that the certificate is invalid by going to [the Vault web UI](https://vault.ritsec.cloud:8200/ui) in your browser.

Next, you can log in with your credentials. The following is an example of a successful login. Replace `YOUR_USERNAME` with your vault username. You will then be prompted for your password - please note that nothing will show up while you are typing. This is normal.

```shell
$ vault login -method userpass username=YOUR_USERNAME
Password (will be hidden): 
Success! You are now authenticated. The token information displayed below
is already stored in the token helper. You do NOT need to run "vault login"
again. Future Vault requests will automatically use this token.

Key                    Value
---                    -----
token                  REDACTED
token_accessor         REDACTED
token_duration         768h
token_renewable        true
token_policies         ["foo" "default"]
identity_policies      []
policies               ["foo" "default"]
token_meta_username    YOUR_USERNAME
```

