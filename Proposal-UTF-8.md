# Proposal 1: UTF-8 as Bio-sequence Encoding

Inclusion of The Unicode Consortium and IUPAC/IUBMB.

# Why UTF-8/Unicode

From the [Unicode FAQ](http://www.unicode.org/faq/basic_q.html):

> Q: What is the scope of Unicode?
>
> A: Unicode covers all the characters for all the writing systems of the world, modern and ancient. It also includes technical symbols, punctuations, and many other characters used in writing text. The Unicode Standard is intended to support the needs of all types of users, whether in business or academia, using mainstream or minority scripts.

This is a clear commitment to science and as bio-sequences are central to biology
and life itself, I believe that "The Unicode Consortium" can be convinced to
dedicate a fair number of code points to nucleic and amino acids.

https://www.unicode.org/standard/standard.html


# Two Possible Ways to Use UTF-8

There exists one way to employ UTF-8 as bio-sequence encoding that requires the
approval of The Unicode Consortium and results in the inclusion of the new
encoding in the Unicode and one that uses the part of UTF-8 that can be
used for custom purposes by anyone - the [Private Use Area](https://de.wikipedia.org/wiki/Private_Use_Area) consisting of 4096
code points (Range: E000-F8FF).



# regex

The bio-sequence analysis with regex could be expanded to include character sets
that make sense for the introduced code points, e.g. for charge, composition and
size.

character sets / character classes


# Modifications


https://www.uniprot.org/help/mod_res
https://www.uniprot.org/help/carbohyd

https://dnamod.hoffmanlab.org/
