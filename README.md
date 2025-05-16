# Github Actions Language Server in Nixos

> This flake exists because there's no easy way to install the Github Actions Language Server in Nixos, and we can't easily use mason.nvim in Nixos either.

A self-updating (every 6 hours) Nix Flake that packages [`lttb/gh-actions-language-server`](https://www.npmjs.com/package/gh-actions-language-server) using [`dream2nix`](https://github.com/nix-community/dream2nix).
Useful for Neovim, editors, or developer tools that rely on Github Actions language intelligence — all fully reproducible and Nix-native.

## 🚀 Usage

### 📥 Install via Flake

> [!note]
> This is just an example, you can use this flake however it suits your configuration style.

```nix
# flake.nix
{
 inputs.nixos-gh-action-ls.url = "github:y3owk1n/nixos-gh-action-ls";

 outputs = { nixos-prismals, ... }: {
  nixosConfigurations.myComputer = pkgs.lib.nixosSystem {
   system = "x86_64-linux";
   specialArgs = { inherit nixos-gh-action-ls; };
   modules = [
    ...
   ];
  };
 };
}
```

Then you can use it in your nixos or home manager configuration:

```nix
# configuration.nix
{
 environment.systemPackages = with pkgs; [
  nixos-gh-action-ls.packages.${pkgs.system}.default
 ];
}

# or home manager
{
 home.packages = with pkgs; [ nixos-gh-action-ls.packages.${pkgs.system}.default ];
}
```

Then use `gh-actions-language-server` as needed (e.g. in your Neovim LSP config).
