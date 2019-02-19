# Introduction


# Proposal to use UTF-8 as standard Encoding for bio-sequences

The introduction gives an overall picture of the problems associated with
the storage and analysis and visualization of modified bio-sequences and how
the expansion of the bio-sequence alphabet alleviates them and why UTF-8 is
the ideal encoding for this expansion.

In case you are not familiar with encodings you can find a small glossary with
the most important terms in the Glassary.md file.


## History and problem statement

To date (January 2019) basically all bio-sequences in public databases are encoded as strings of single letters. Nucleic acids and amino acids are represented by letters and to ensure the unambiguous translation from molecule to string and vice versa it is a bijective projection. The single letter codes for bases and amino acids used today are defined by IUPAC and are letters of the English alphabet that can be encoded in ASCII. The choice to use ASCII as the underlying encoding probably was not much of a choice, but the only reasonable way to encode the strings to make the sequences shareable across computing platforms worldwide. ASCII works well because IUPAC mapped all nucleic acids and amino acids to characters in the ["ISO basic Latin alphabet"](https://en.wikipedia.org/wiki/ISO_basic_Latin_alphabet)  with its 26 letters (52 - if you count capital and small letters separately). All letters in this alphabet are now mapped in the protein context and no new amino acid or modified amino acid can be encoded any more without breaking the unique assignment of one chemical entity per letter.

The study of posttranslational modifications (PTMs) in proteins is growing fast, as more modifications are found and the methods to find and measure them are generating ever more data.

There is a desire to study modified sequences with the same tools already available for non-modified sequences, such as sequence alignments, sequence motive detectors, and visualization software. Sequences are also often compared by eye which requires intuitive representation of sequences on screens and on paper. For this purpose, it is important that the representation of amino acids and nucleic acids remains a single glyph* to avoid misleading apparent frameshifts. Avoiding frameshifts in the encoding is desired to continue the use of sequence analysis software available to date.


## Possible reactions to the modified sequence problem

### Continue using ASCII 1: Map the rest of the ASCII table printables to modified acids

There are only 127 ASCII code points and some of them have special meanings, such as controls and spaces (including tab, linebreak) which leaves us in the best case 93 codes. IUPAC already defines 26 Amino acid codes. The remaining 67 free codepoints are - not nearly enough to encode the 647 PTMs recorded in the UniProt https://www.uniprot.org/docs/ptmlist file. Although I can not predict how many codes find their way into sequences in the near future, at some point, all of them probably will.
Another problem with this approach is that the use of capital and small letters can lead to sequences that might look like sequences in three letter codes, but represent a sequence in the extended ASCII sequence encoding.


### Continue using ASCII 2: Normalize the use of multi-letter codes

This is probably the worst proposal since it would increase the storage size of sequence information and most bioinformatics software expects single-letter codes. So the main drawbacks are the increased use of storage and limited bioinformatics tools that can handle the format.

### Binary/enum formats?

When saved and shared, DNA can in principle encoded with two bits. This is results in a very efficient storage format but requires an additional definition of the mapping of numbers to acids.
@Peter: do you know if and how this is used in practice nowadays?

The addition of more codes leads to changes in the number of bits necessary to encode the chemical entities and this can lead to a multitude of different encodings. The use of different encodings is a recipe for confusion, parsing errors and ultimately data loss coupled with breaking or even false analytics and should be avoided. (The reason I write this is the troubles people experienced when exchanging text files on the web over language barriers in the time before UTF-8 became the de facto standard for plain text files on the web.)


### Mappin modified acids to UTF-8 codepoints

Generally, there is a desire to encode modified amino acids in single characters. This desire stems from practical issues like comparing sequences by eye - if the modified sequence is longer than the non-modified, there is a shift and the comparison becomes difficult. This is also the case for sequence alignment algorithms that would have to be able to specifically cope with the modifications.
The use of UTF-8 potentially allows the unique mapping of >2.000.000 chemical entities to code points in a text format that is machine- and human readable. It also is a superset of ASCII which contains all the single-letter codes that are already defined by IUPAC and thus supports the old sequence file format out of the box - old files don’t become obsolete.


## Long term view

The long term readability of the data is an important factor when considering sequence information representations and storage. The main factors here are hardware and software evolution. Since UTF-8 is the de facto standard for text, most programming languages and basically all operating systems can handle it really well and efficiently.


## Future encoding changes

Changing or expanding the encoding for biological sequences is a big endeavor because it can break backward compatibility - new sequence files may not be used in old bioinformatics tools. Many software tools in use today might not work out of the box with UTF-8 encoded sequences.


## Comparison of discussed approaches (Maybe better done in a Table?)


### UTF-8

### Pros

* Well defined
* Most software handles it well
* Well tested for real-world applications
* Efficient storage format (not much larger than ASCII)

### Cons

* Not all algorithms may read UTF-8
* "New" to the community


## Enum

### Pros

* Well defined / defined per use case
* Well tested for real-world applications
* Efficient storage format

### Cons

* requires separate encoding definitions.
* requires specific parsers


# Conclusion

The desire to efficiently encode PTMs and being able to handle them in a straight forward manner in all bioinformatics workflows is highly desired. The current encoding system does not allow this and there needs to be a considerable effort to make the change and at the same time prevent an encoding jungle where many encodings emerge and incompatibilities are generated unnecessarily. Because of all the reasons discussed above, I believe that the use of UTF-8 as a bio-sequence format is not just reasonable but inevitable.

If the proposal finds support there should be a more general discussion within the bioinformatics community including EBI/SIB/IUPAC (add more institutions as required.). At some point of this discussion, we might profit from the help of people from the Unicode Consortium with their vast knowledge of encodings and expanding alphabets.

# Finally

Thank you for your interest, time and brainpower! Whether you support the proposed use of UTF-8 for bio-sequence encoding or object to it, your inputs and feedbacks are much desired!
