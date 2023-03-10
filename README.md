# Installing dependencies

The Coq development requires Coq version 8.13.2 and OCaml 4.13.1.

We modified the Verimag Polyhedra Library.

Some additional C and OCaml libraries are required, as described below.

We recommend to use either OPAM (the OCaml package manager) or Nix (a Linux package manager).

## With OPAM 

Create a new OPAM switch: `opam switch create polygen 4.13.1`.
Install GMP, Debian/Ubuntu package libgmp-dev
Install GLPK, Debian/Ubuntu package libglpk-dev
Install [eigen](http://eigen.tuxfamily.org/), Debian/Ubuntu package libeigen3-dev.
Install the following ocaml packages: `opam install zarith glpk menhir coq=8.13.2`.

## With Nix

Another way is to use `nix`. Type `nix-shell` to get a shell where all dependencies have been downloaded and installed.
One way to install `nix` is:
```bash
curl https://nixos.org/nix/install | sh
```

Note that, if you use OPAM, the OPAM init scripts can add your current version of ocaml to your `$PATH`. In that case, it is advised to use
`nix-shell --pure`, which will run a shell where all dependencies have been downloaded and installed, but no other programs will be available,
avoiding the conflicts with a preexisting OPAM installation.

# Compiling

There are four steps for compiling the code:
* Setup the VPL: `make vplsetup`.
  This step compiles the bundled version of the Verimag Polyhedra Library that we use.
* Compile the Coq files: `make`.
* Extract the code generator to OCaml: `make extract`.
* Compile the extracted code: `make ocaml`.

The executable running the code generator on different tests will be in `ocaml/test`.  Just run `./ocaml/test`, the results will be displayed on standard output.

Alternatively, if using `nix`, you can just type `nix build`, and the executable will be available in `result/bin/test`.

You can build the documentation with `make documentation`, and it will be available in doc/index.html, or result/doc/index.html if you used `nix build`.