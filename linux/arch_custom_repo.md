# Arch Linux custom repository
- Create a repository in a git host. Ex `arch-repo`
- Create a folder **x86_64** (for 64 bits)
- Inside **x86_64** the pkg.tar.zst files of the programs generated with makepkg command
- Inside **x86_64** execute `add-repo arch-repo.db.tar.gz *pkg.tar.zst`
- Delete the symbolic links
- Rename **arch-repo.db.tar.gz** and **arch-repo.files.tar.gz** removing the **tar.gz** suffix

## Add to Pacman
- Add in `/etc/pacman.conf`
```bash
[arch-repo]
SigLevel = Optional TrustAll
Server = https://raw.githubusercontent.com/javiorfo/$repo/refs/heads/master/$arch
```
