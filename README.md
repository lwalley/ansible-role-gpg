# Ansible Role: GPG

Generate keys with [gnupg2][gnupg2] on macOS.

## Requirements

[gnupg2][gnupg2] must be installed on the system prior to running this role
(suggested role: `geerlingguy.homebrew`).

## Role Variables

Available variables with example values are listed below, for default values see
[`defaults/main.yml`](defaults/main.yml)). Keys listed in `gpg_keys` will be
created using [unattended key generation][gpg-unattended]:

    gpg_keys:
      # Lookup is used to determine whether or not a key exists in the output
      # of gpg --list-keys --with-colons, and won't create the key if it does.
      - lookup: "marvin@depressed-androids.io"
      # Config contains key value array pairs that will be output as is to the
      # file passed into `gpg --generate-keys --batch`.
      - config:
        - [ "Key-Type", "default"]
        - [ "Subkey-Type", "default" ]
        - [ "Name-Real", "Marvin the Paranoid Android" ]
        - [ "Name-Email", "marvin@depressed-androids.io" ]
        - [ "Expire-Date", 0 ]
        - [ "Passphrase", "I'm so depressed" ]

## Dependencies

None.

## Example Playbook

    - hosts: localhost
      roles:
         - { role: lwalley.gpg }

## License

MIT

[gnupg2]: https://gnupg.org
[gpg-unattended]: https://www.gnupg.org/documentation/manuals/gnupg/Unattended-GPG-key-generation.html
