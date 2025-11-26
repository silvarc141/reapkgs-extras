# reapkgs-extras

This repo repackages an arbitrary list of ReaPack indexes (in repos.txt) using [reapkgs](https://github.com/silvarc141/reapkgs) for the nix / home-manager ecosystem.  

This repo may also serve as a template for your own reapkgs repo.

>[!Warning]
>Package data generation is automated, this flake provides no additional vetting of packages.

## Usage

### Home Manager

(in flake.nix)
```nix
{
  inputs = {
    # ...
    reapkgs-known.url = "github:silvarc141/reapkgs-known";
  };
}
```

(in home.nix)
```nix
xdg.configFile.REAPER = {
  # join all packages in REAPER config path to preserve correct directory structure
  recursive = true;
  source = pkgs.symlinkJoin {
    name = "reapkgs";
    paths = with inputs.reapkgs-known.legacyPackages.${pkgs.system}; [
      # add packages
      # index-name."package-name"
      saike-tools."saike_abyss.jsfx"
    ];
  };
};
```

## Contributing

If you want an index url to be included, add it to repos.txt and make a PR.
