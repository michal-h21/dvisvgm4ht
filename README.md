# Alternative TikZ drivers for tex4ht

This repository contains two alternative TikZ drivers for `tex4ht` which tries to fix some issues with the default driver distributed with TikZ. Among these issues are:

- [wrong text formatting after TikZ pictures](https://tex.stackexchange.com/q/257559/2891)
- [issues with text encoding](https://tex.stackexchange.com/q/390592/2891)
- [compilation errors](https://tex.stackexchange.com/q/386757/2891)



## pgfsys-dvisvgm4ht.def

The first driver one uses `dvisvgm` for the SVG file creation, resulting in higher quality graphics. The extra step with `dvisvgm` invocation can result in longer compilation time, but the result is usually better, than with the default driver.

### Usage

Put following lines before TikZ package loading:

    \ifdefined\HCode
      \def\pgfsysdriver{pgfsys-dvisvgm4ht.def}
    \fi 

# pgfsys-tex4ht.def

The second driver is updated original `tex4ht` driver. It will be used by default when properly installed. Note that if you use complex text nodes, like math contents, better results can be obtained using `escape=true` option. This option can be set globally in the custom configuration file:

    \Preamble{xhtml}
    \tikzset{every node/.style={/pgf/tex4ht node/escape=true}}
    \begin{document}
    \EndPreamble

It can even support MathML output in SVG. Which is unfortunately supported only by Firefox. 


## Installation

Clone this repository to a `tex/latex` subdirectory in your local `TEXMFHOME` tree. For example:

     ~/texmf/tex/latex/dvisvgm4ht/

Read more about [TEXMFHOME](https://tex.stackexchange.com/a/271545/2891).
