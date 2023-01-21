# Gentoo Monero Overlay

Up-to-date fork of the gentoo overlay of the monero software as of 20/12/2022 (v0.18.1.2).

## Getting Started

### Manual

```bash
# Add overlay to repos.conf.
cat << EOF > /etc/portage/repos.conf/monero.conf
[monero]
location = /var/db/repos/monero
sync-type = git
sync-uri = https://github.com/Linus-J/gentoo-monero.git
EOF

# Sync the overlay.
emaint sync --repo monero

# Unmask everything in the overlay.
#Option 1: (If your package.accept_keywords is a directory)
echo '*/*::monero ~amd64' >> /etc/portage/package.accept_keywords/monero
#Option 2: (If your package.accept_keywords is a file)
echo '*/*::monero ~amd64' >> /etc/portage/package.accept_keywords

# Install some software! (::monero ensures installation from the newly created local monero repo)
emerge -a net-p2p/monero::monero 
```

## Package Upgrades
```bash
# Sync the local repo with the current overlay.
emaint sync -r monero 
# The above command will execute during a standard emaint -a sync. Only need to use when specifically updating this repo.

# Upgrade packages as usual.
emerge -avuDN @world
```

## Package removal
```bash
# Deselect package via portage and remove unused dependencies safely
emerge --deselect net-p2p/monero::monero
emerge -a --depclean

# Reomve overlay from repos.conf.
rm -i /etc/portage/repos.conf/monero.conf

# Remask everything from the overlay.
#Option 1: (If your package.accept_keywords is a directory)
rm -i /etc/portage/package.accept_keywords/monero
#Option 2: (If your package.accept_keywords is a file)
sed -i '/\*\/\*::monero ~amd64/d' /etc/portage/package.accept_keywords
```

## Contributing
Linus-J:
This is my first time working with gentoo overlays, so if there is any good/common practices I have diverted from in this fork feel free to submit a pull request or an issue and I'll do my best to sort it out.

From original:
Contributions of all types are welcome.
Feel free to make a pull request!
See [CONTRIBUTING.md](CONTRIBUTING.md) in the project root for more info.


