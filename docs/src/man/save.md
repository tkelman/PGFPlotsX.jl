#  Showing / Exporting figures

## Jupyter

Figures are shown in .svg format when evaluated in Jupyter. For this you need the `pdf2svg` software installed.

## REPL

In the REPL, the figure will be exported to a pdf and attempted to be opened in the default pdf viewing program.
If you wish to disable this, run `pgf.enable_interactive(false)`.

## Exporting

Figures can be exported to files using

```jlcon
pgf.save(filename::String, figure; include_preamble::Bool = true)
```

where the file extension of `filename` determines the file type (can be `.pdf`, `.svg` or `.tex`) and `include_preamble`
sets if the preamble should be included in the output (only relevant for `tex` export).

## Customizing the preamble

It is common to want to use a custom preamble to add user-defined macros or different packages to the preamble. There are a few ways to do this:

* `push!` strings into the global variable `CUSTOM_PREAMBLE`. Each string in that vector will be inserted in the preamble.
* Modify the `custom_premble.tex` file in the `deps` folder of the directory of the package. This file is directly spliced into the preamble of the output.
* Define the environment variable `PGFPLOTSX_PREAMBLE_PATH` to a path pointing to a preamble file. The content of that will be inserted into the preamble.

## Choosing the LaTeX engine used

Thee are three different choices for latex engines, `PDFLATEX`, `LUALATEX` and `XELATEX`.
By default, `LUALATEX` is used. The active engine can be retrieved with the `latexengine()` function and be set with `latexengine!(engine)` where `engine` is one of the three previously mentioned engines.

## Custom flags

Custom flags to the engine can be used in the latex command by `push!`-ing them into the global variable `CUSTOM_FLAGS`.
