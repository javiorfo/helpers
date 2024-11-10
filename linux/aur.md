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
git clone ssh://aur@aur.archlinux.org/my_program.git
```
- Put inside a PKGBUILD file. [Example]()
- Execute the command
```bash
makepkg --printsrcinfo > .SRCINFO
```
- Push the repo
