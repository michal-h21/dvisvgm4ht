# pgfsys-dvisvgm4ht.def

This repository contains alternative TikZ driver for `tex4ht`. It uses `dvisvgm` for the SVG file creation, resulting in higher quality graphics and it avoids some issues with default `tex4ht` TikZ driver:

- wrong formatting of font changes in the document following a TikZ picture
- issues with complex text formatting in Tikz Nodes
- compilation errors


Usage: 

Put following lines before TikZ package loading:

    \ifdefined\HCode
      \def\pgfsysdriver{pgfsys-dvisvgm4ht.def}
    \fi 

Installation:

Place `pgfsys-dvisvgm4ht.def` into `tex/latex/dvisvgm4ht` directory inside your local `TEXMFHOME` tree. For example:

     ~/texmf/tex/latex/dvisvgm4ht/pgfsys-dvisvgm4ht.def

Read more about [TEXMFHOME](https://tex.stackexchange.com/a/271545/2891).
