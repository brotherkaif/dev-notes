**ID:** 1202212230212
**STATUS:** #permanent-note
**TAGS:** #git

---

# How to Update User Config in Git
1. In your terminal, navigate to the repo you want to make the changes in.
2. Execute `git config --list` to check current username & email in your local repo.
3. Change username & email as desired. Make it a global change or specific to the local repo:
```bash
git config [--global] user.name "Full Name"
git config [--global] user.email "email@address.com"
```
4. Per repo basis you could also edit `.git/config` manually instead.

---
## References
1. [How to change my Git username in terminal?](https://stackoverflow.com/a/36782014)