# Alternative TikZ drivers for tex4ht

This repository contains two alternative TikZ drivers for `tex4ht` which tries
to fix some issues with the default driver distributed with TikZ. Among these
issues are:

- [wrong text formatting after TikZ pictures](https://tex.stackexchange.com/q/257559/2891)
- [issues with text encoding](https://tex.stackexchange.com/q/390592/2891)
- [compilation errors](https://tex.stackexchange.com/q/386757/2891)



## pgfsys-dvisvgm4ht.def

The first driver one uses `dvisvgm` for the SVG file creation, resulting in
higher quality graphics. The extra step with `dvisvgm` invocation can result in
longer compilation time, but the result looks usually better than with the
default driver.

This driver is a preferred option, as the resulting SVG files usually look
identical to the produced PDF.

If you have lot of figures in your document, their compilation by Dvisvgm can
take lot of time. You can speed it up using the `dvisvgm_hashes` extension for `make4ht`:

    make4ht -f html5+dvisvgm_hashes filename.tex

It compiles only changed figures on subsequent compilation runs.

The driver has two modes. The default one supports complex images, but it has
some issues with patterns. To fix that, you can try the `tikz+` option. 
This option supports patterns and it should produce the same result in most cases,
but it can fail with more complex pictures.


## pgfsys-tex4ht-updated.def

The second available driver is a modified version of the original `tex4ht`
driver. It doesn't rely on external tools for the conversion, so the compilation can
be faster. The downside is that the resulting SVG file can look quite different
from expected.

Note that if you use complex text nodes, like math contents, better
results can be obtained using `escape=true` option. This option can be set
globally in the custom configuration file:

    \Preamble{xhtml}
    \tikzset{every node/.style={/pgf/tex4ht node/escape=true}}
    \begin{document}
    \EndPreamble

It can even support MathML output in SVG. This SVG output is unfortunately
supported only by Firefox. 

# Usage

Put following lines to your document preamble, before lines where the TikZ
package is loaded:

    \ifdefined\HCode
      \def\pgfsysdriver{<drivername>}
    \fi 

For example document that use the `dvisvgm` driver should use the following
structure:

    \documentclass{article}
    \ifdefined\HCode
      \def\pgfsysdriver{pgfsys-dvisvgm4ht.def}
    \fi 
    \usepackage{tikz}
    \begin{document}
    ...
    \end{document}

# Installation

Clone this repository to a `tex/generic` sub directory in your local `TEXMFHOME`
tree. For example:

     ~/texmf/tex/generic/dvisvgm4ht/

Read more about [TEXMFHOME](https://tex.stackexchange.com/a/271545/2891).
