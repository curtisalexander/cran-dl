# cran-dl
Download an R package as a tarball from CRAN.  Able to download either the current version or an archived version.

## Requirements
Makes use of the following packages.  `devtools` is only required in order to install `docopt`.

```R
devtools::install_github("docopt/docopt.R")
install.packages("httr")
install.packages("purrr")
install.packages("rvest")
install.packages("xml2")
```

## Usage

```bash
cran-dl --pkg=<pkg> [--version=<version>] --path=<path>
cran-dl -h | --help
```

## Options

```bash
--pkg=<pkg>             R package name
--version=<version>     [Optional] R package version to download
--path=<path>           Directory path to save tar.gz file
-h, --help              Help
```

## Example

```bash
# download current version of dplyr
cran-dl --pkg=dplyr --path="~/code/r-pkgs"

# download archived version, 0.4.3, of dplyr
cran-dl --pkg=dplyr --version=0.4.3 --path="~/code/r-pkgs"
```

## Use Case
When working on particular servers, I have need to install specific package versions from CRAN.  The only way to install a package is to download the package as a `tar.gz` file from a different machine, copy it to the server, and perform a local install on the server.

I typically save downloaded packages as `tar.gz` files in a common directory.  This allows me to execute code similar to that below to install the package.

The code below will also allow me to install a locally developed package without needing to remember the exact version number. I simply replace the locally developed package in the directory with the latest version.

```R
# install sparklyr package
pkg_dir <- "~/code/r-pkgs"
tgz_file <- list.files(path = pkg_dir,
                       pattern = "^sparklyr",
                       recursive = FALSE)
pkg <- file.path(pkg_dir, tgz_file)
devtools::install_local(pkg)
```

## Related
See [gh-dl](https://github.com/curtisalexander/gh-dl) which allows one to download R packages from Github.
