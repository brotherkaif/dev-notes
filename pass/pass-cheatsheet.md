# Creating a password store
You will need to first create a GPG key that will be used to encrypt the store
```
pass init GPG-ID
```
This will create an encrypted `.password-store` in the root directory

# Version control
The `.password-store` is encrypted with your GPG key so it is (relatively) safe to have this managed as a git repository. You can go ahead and run a `git init` inside the directory and mangage it like any other repository.
