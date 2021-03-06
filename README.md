# r-dyntrace

This aims to be a flexible R distribution based on docker that includes all CRAN and BIOC packages.
Currently it is tested on R 3.5.0 and R-dyntrace.

## Setup

1. choose which R to use and go to the proper directory

2. create the base docker images `prlprg/r-common`:

```sh
$ make image
```

3. create a docker volume `r-cran-mirror` containing a CRAN mirror:

```sh
$ make cran-mirror
```

3. create a docker volume `r-cran-lib` containing all CRAN packages installed using the chosen R version:

```sh
$ make cran
```

4. (optional) create a docker volume `r-cran-src-extracted` containing extracted CRAN packages that were installed in `r-cran-lib`:

```sh
$ make cran-sources
```

5. create a docker volume `r-bioc-lib` containing all BIOC packages installed using the chosen R version:

```sh
$ make bioc
```

6. (optional) create a docker volume `r-bioc-src-extracted` containing extracted BIOC packages that were installed in `r-bioc-lib`:

```sh
$ make bioc-sources
```

## Usage

To run the image you can do:

```sh
make exec COMMAND="<cmd>"
make bash
make zsh
make r
make rscript SCRIPT="<script>"
```

There are following directories:

- `/R` - R sources and binaries (to run R just do `/R/bin/R` from within the
  container) - it is mounted from the local `R` directory
- `/CRAN/lib` - installed CRAN packages
- `/CRAN/src-extracted` - extracted CRAN package sources
- `/CRAN/src` - CRAN mirror
- `/BIOC/lib` - installed BIOC packages
- `/BIOC/src` - downloaded BIOC package sources
- `/BIOC/src-extracted` - extracted BIOC package sources

