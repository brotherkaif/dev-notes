# NIX: Cheatsheet

## MacOS: Setup Guide

Install Nix Package Manager:

```bash
% sh <(curl --proto '=https' --tlsv1.2 -L https://nixos.org/nix/install)
```

Test that it's working (in a new session):

```bash
% nix-shell -p neofetch --run neofetch
```

Create a new Nix flake:

```bash
% mkdir ~/.config/nix
% cd ~/.config/nix
% nix flake init -t nix-darwin --extra-experimental-features "nix-command flakes"
```

Update the generated config (e.g. change description and config name) and then build the flake (in this case, the `mini` config is being built):

```bash
% sudo nix run nix-darwin --extra-experimental-features "nix-command flakes" -- switch --flake ~/.config/nix#mini
```

Verify installation:

```bash
% which nix-darwin
```

To rebuild after changes to the nix config:

```bash
% darwin-rebuild switch --flake ~/.config/nix#mini
```

## Resources

- [Nix is my favorite package manager to use on macOS](https://youtu.be/Z8BL8mdzWHI?si=Zwn5DpPAuI7phz1N)
