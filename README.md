# Yubikey teknisk demo

![yubikey image](https://media.yubico.com/media/catalog/product/y/k/yk5c-hero-2020.png)

- SSH
- Signerte commits
- 2FA
- Og mye mer

## Setup
🤔 Generere masterkey på eller av nøkkelen?

**Best** (men _litt_ :tinfoil:) [DrDuhs guide](https://github.com/drduh/YubiKey-Guide)

**Enklest**: [Yubikey all the things](https://www.engineerbetter.com/blog/yubikey-all-the-things/)  


## SSH
### Installer gpg

`$ brew install gpg`

### Bytte pin og adminpin

Default er  123456/12345678

```
$ gpg --change-pin
```
💡Husk din nye adminpin!

### Få maskinen din til å bruke GPG-agent
øverst i `.zshrc`eller `.bashrc`:

```
    │ File: .zshrc
────┼──────────────────────────────────────────────────────
1   │ export GPG_TTY=$(tty)
2   │ gpg-connect-agent updatestartuptty /bye
3   │ unset SSH_AGENT_PID
4   │ export SSH_AUTH_SOCK=$(gpgconf --list-dirs agent-ssh-socket)
```

### Installer et gui for å skrive inn pin

`$ brew install pinentry-mac`

```
    │ File: .gnupg/gpg-agent.conf
────┼────────────────────────────────────────────────────
1   │ pinentry-program /usr/local/bin/pinentry-mac
2   │ default-cache-ttl 0
```

### Generer RSA key
* on key https://www.engineerbetter.com/blog/yubikey-ssh/#roca
* off key https://github.com/drduh/YubiKey-Guide#master-key


## 2FA
  * https://github.com/settings/two_factor_authentication/configure

## Signerte commits

### Få tak i din public key om du ikke har den lokalt
`$ gpg --keyserver keys.openpgp.org --search <email>`


###Eksporter til Github
* Finn `<key>`: `$ gpg --list-secret <email>`
* Eksporter: `$ gpg --armor --export <key>`
* Lim inn: https://github.com/settings/gpg/new
* Fortell Git hva du driver med:
```
git config --global commit.gpgsign true
git config --global user.signingkey <key>
```

https://github.com/trulsjor/yubikey/commits/main
