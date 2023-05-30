# Pacman
- Update database: `sudo pacman -Syy`
- Total remove: `sudo pacman -Rsc package`
- Info: `sudo pacman -Qi package`
- Installed packages: `sudo pacman -Qn`
- Available local package: `sudo pacman -Qs package`
- List all files from a package: `sudo pacman -Ql package`
- List unused: `sudo pacman -Qtdq`
- Remove unused: `sudo pacman -R $(pacman -Qtdq)`
