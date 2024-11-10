# Create package for AUR Arch Linux

## AUR Steps
- Create an account
- Create a SSH public key
```bash
ssh-keygen -t rsa -b 4096 -C "mail@mail.com"
```
- Copy and paste the result of **cat .ssh/id_rsa.pub** in SSH public key from AUR profile

## PC Steps
- create a repo named as the program itself
```bash
git clone ssh://aur@aur.archlinux.org/myprogram.git
```
- Put inside a PKGBUILD file. [Example](https://github.com/javiorfo/helpers/blob/master/linux/PKGBUILD)
- Create a binary compressed using
```bash
tar -czf myprogram-0.1.0.tar.gz myprogram-0.1.0/
```
- Create a sha512 executing
```bash
sha512sum myprogram-0.1.0.tar.gz
```
- Execute the command
```bash
makepkg --printsrcinfo > .SRCINFO
```
- Push the repo
