# GPG: Key Management and Encryption

## Generate Keys
```
gpg --full-generate-key
gpg --full-gen-key
```
Generate a new key pair with dialogs for all options.  This is an extended version of `--generate-key`.

## Import Keys
```
gpg --import KEY_FILE
```
Import/merge keys. This adds the given keys to the keyring. The fast version is currently just a synonym.

## List Keys
```
gpg --list-keys
gpg --list-secret-keys
gpg -k
```
List the specified public/private keys.  If no keys are specified, then all keys from the configured public keyrings are listed.

## Trust Keys
```
gpg --edit-key KEY_ID
gpg> trust
```
Present a menu which enables you to do most of the key management related tasks.  It expects the specification of a key on the command line.

## Export Keys
```
gpg --export -armor KEY_ID > KEY.pub.asc
gpg --export-secret-keys -armor KEY_ID > KEY.asc
```
Either export all keys from all keyrings (default keyrings and those registered via option `--keyring`), or if at least one name is given, those of the given name. The exported keys are written to STDOUT or to the file given with option `--output`.  Use together with `--armor` to mail those keys.

## Delete Keys
```
gpg --delete-keys KEY_ID
gpg --delete-secret-keys KEY_ID
```
Allows you to delete keys from your system.

## Encrypt
```
gpg --encrypt --armor --recipient KEY_ID INPUT_FILE
gpg -ear KEY_ID INPUT_FILE
```
Encrypt data to one or more public keys. This command may be combined with:
- `--sign`: To sign and encrypt a message
- `--symmetric`: To encrypt a message that can decrypted using a secret key or a passphrase
- `--sign` and `--symmetric`: For a signed message that can be decrypted using a secret key or a passphrase
- `--recipient` and related options: specify which public keys to use for encryption

## Decrypt
```
// with a file
gpg --decrypt INPUT_FILE > OUTPUT_FILE

// with a heredoc
gpg --decrypt << EOF
-----BEGIN PGP MESSAGE-----
lksjdflskdjflsdkfjsldkfj...
-----END PGP MESSAGE-----
EOF
```
Decrypt the file given on the command line (or STDIN if no file is specified) and write it to STDOUT (or the file specified with `--output`). If the decrypted file is signed, the signature is also verified. This command differs from the default operation, as it never writes to the filename which is included in the file and it rejects files that don't begin with an encrypted message.

## Verify
```
// with a file
gpg --verify INPUT_FILE

// with a "here" file
gpg --verify << EOF
[content]
EOF
```
Will verify the signature of the message provided against a key on your system.
