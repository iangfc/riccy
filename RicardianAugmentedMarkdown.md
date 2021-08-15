
# Ricardian Augmented Markdown

 * Version = 0.0.2

This format for Ricardian contracts is compatible with and layered over the
[GitHub Flavoured Markdown Spec](https://github.github.com/gfm/).
Part of this project is to experiment with the use of github editing
as a collaboration tool for programmers to write Ricardian contracts,
so it is natural to rely on that specification; but it is likely that
other [Markdowns](https://commonmark.org/) work as well.

The format - RicardianAugmentedMarkdown or RAM for now
is designed to allow a simple line-based parser to extract
what it needs and not require complicated processing typical of sophisticated grammars.
Note that this layer sees through most of the Markdown formatting, as formatting is not it's job.

## Tag-value Parameters
A basic parameter is a line with
 + a star (bullet list item),
 + a single (program language style) tag word,
 + an assignment symbol, which can be one of:
     + equals symbol = or,
     + a plus-equals symbol +=, and
 + whatever comes after that until end of line (or a comment symbol XXX unimplemented).

The presence of = or += in a star bullet list is a trigger, and has to be formatted correctly with at least a space between the bullet and tag, and a space between the tag and the symbol. If there is no value, then the second space can be missing (and will be stripped anyway by canonicalisation).

Params come in two forms. Fristly as a specific one line assignment using star bullet lists
(and in 2 variants):

 * Tag = some value words, until eoln.
 + which bullets can be intermingled inside a list...
 * TAG_2 = can have some more value words.
 + The second form is the array form:
 * Tag-3.array += Using += signals that this Tag-3 has an array or multivalue form,
 * Tag-3.array += which is useful for routing to URLs that are replicated.
 * Tag.4.singleton = You can mix += symbols, the first one counts.
 * Whitespace = you must have at least a space after the star bullet and before the symbol (after the symbol is optional because canonicalisation will trim an empty value back to the symbol

The above shows all legal tags.  Others include t.a.g

The rules for tag naming are similar to programming languages:
 * Tags start with an alpha [a-zA-Z].
 * Tags end with an alphanumeric [a-zA-Z0-9].
 * Tags contain also numerals (not in first character) and three symbols hyphens, fullstops and underscores [a-zA-Z0-9_-.] (not in first or last character).
 * Tags are Case Sensitive; "Oh, East is East, and west is west, and never the twain shall meet." Devs are familiar with this concept, and I am [reliably informed](https://twitter.com/CommonAccord/status/1421570064206090242) that lawyers are careful too.
 * Be careful with underscores in the tag name as they can also be interpreted as emphasis by markdown.

Illegal tags would include 1bad, -bad, bad#tag, .bad or bad_ or bad= .  XXX Don't duplicate the punctuation, as that will likely be enforced as bad: dupli__cated..punct-._ation would be bad.

### Multiline tagged paragraphs

*Multiline* A paragrah can be tagged as a multiline,
which starts with an emphasised tag word, in this case
the tag Multiline will have these 3 lines.

*Closure* Following the tag line is any number of lines of text, including paragraphs and empty lines.
The multiline format is always closed by
  + a new section, like this one for Multiline above,
  + the end of file, or
  + two or more stars on its own line followed by an empty line or other block closer, as follows this very line.
Sadly, when markdown renders its formatting on double-star,
it folds all these lines into one para, so it ends up displayed on the end of line, not the next line.
No matter, *remember* to place the double-star on its own line in the raw text:
**

*Closed.*  See! In the Ricardian, the above is now closed and a new one is opened, called Closed.
It has to have the closing marker by itself on its own line to avoid the
Ricardian parser doing strange things.  Another way to close it is to use three or more stars:
***

Which should trigger a line in HTML in the displayed text.  Let's see.

***And_More_Emphasis*** Also note that more emphasis is allowed for the
open of a multiline, as long as it is a legal set using only star, and not underscore.
That's because it is a common pattern in coding to use underscores inside names, like this_thing.
This should be done carefully by the author as the Markdown parser sees underscores as emphasis_.
****
*FullStop.* You can also put a single fullstop at the end of the tag name for style.
This will be stripped off, it is not part of the tag.

*Applicability.* The Multiline hasn't been used much in the past for contractual writing,
but there are certain key elements in contracts that need it.

## Comments
HTML comments <!-- like this one --> are implemented in a partial form:
 
 - no comments before start or after sig/end
 - only one comment (pair or begin or end) per line
 - any tag assignments inside comments must be ignored

Hence the following are legal:
 * <!-- this is a comment -->
 * <!-- this is a multiline
comment that doesn't end until -->

Whereas these are not legal:
 + <!-- one --> and <!-- two --> multiple comments on one line
 + <!-- starts on one line
 + ends on this line --> but <!-- starts again on the same line
 + before ending! --> and vice versa
 + <!-- a comment with a comment start in it: <!-- -->

Comments of a HTML form are much harder because they can cross lines,
and we do want to impose a DOM model
nor a look-ahead parser on the coder, hence there are the above limitations
to make it easier for a simple line based parser.

Comments are not a normal legal convention but I have found that comments are very useful;
this may reflect a different mindset coming from a CS background, where we comment our code!
The meaning of comments is ultimately found in dispute resolution, but
the suggestion herein is that they are not a legally binding part of the contract.
For this reason, it is useful for the comment to be treated as 'softer' by the markdown.

## Headings

### Formats
Headings should be in strict ATX format, that is as above with leading hashes.
SETEXT headings are not supported (those with a line underneath)
which is to say they are ignored by the Ricardian parser.
The only import of this is that the Primary Heading (below) must be a single hash heading.

### (TBD) Heading Tags
I like the idea of automatically tagging the headings with eg 1.2 or 3.4.
But is it worth it to do such complications?

Another possibility is to insert tag names into the headings, as with the multiline paragraph.

## Details

### Whitespace
Only spaces should be used where whitespace is indicated, such as surrounding the tag in a parameter.

### Canonicalisation
In order to assist repeatable hashing so that the document has one clear message digest as an identifier,
the document is canonicalised before hashing and before signing.
Canonicalisation is these rules:
 1. All empty lines before the primary header and after the signature trailer are removed.
 2. All whitespace including end of line characters is removed from the end of every line.
 3. Every line has a newline '\n' or 0x0a added to it.

Note that this differs from previous rules in a couple of ways. Firstly, prior generations used MS end of line "\r\n" as the hashing line terminator. But MS tools don't surface that ending any more whereas the ending (and text formatted documents) are still prevalent in Linux/Mac/Unix platforms. Secondly, every line gets a line ending, unlike OpenPGP which dropped the last one. Having a separate rule for the last line is just a nuisance to the coder.

### UTF
No UTF supported as yet.

## EBNF

Or in EBNF if I can recall my crusty CS:


    Parameter = "*", identifier , "=", value [ "#" , text ], "\n" ;

    Parameter = "*", identifier, [.], "*", [lines], "**", "\n" ;

    lines = [words], "\n" ;

    Variable = "{{", Parameter, "}}" ;

    Identifier = firstletter, [letters], lastletter

    firstletter = [a-zA-Z_]

    letter = firstletter | [-0-9]

    lastletter = firstletter | [0-9]

## Begin and End
Having a defined start and end makes it easy for line-based parsers to look
at what format a file might be in.

### Start Heading
The Ricardian must start with a single one-hash non-empty heading as the first line (after empties, which must be stripped out) as is shown at top of this file.
This first primary Heading is essential to signal that this is a RAM file,
and to initiate the start of hashing.

0-3 spaces leading is OK, more will cancel the heading (TBD).
Always have one space after the leading hashes (TBD).
Optional hashes after a space are stripped from the name/heading in formatting/presentation (TBD).

### End Sig
The Ricardian is ended by the paramater SIG being the signature of the contract
by the issuer.
NB, as with the first heading, this defines the end of hashing.

It can be an empty signature; what this means to higher layer code is undefined,
but at least it can still be hashed.  This allows for unsigned inclusions such
as standard terms and conditions to be composed into a wider agreement.

#### Multiple Signers (TBD)
The possibility of multiple signatures exist by using the += array parameter form,
but are not defined as yet.

<!-- Commentary: Multiple sigs could be treated as counterparts - each over the primary
body, and together forming an agreement. In this case, they could be appended at the end
of the file, and stripped off for signing; the signature should be constructed over
the file with only the one last-line containing the empty * SIG +=.

Then, each additional signer could strip off the existing sigs, sign, and then add their
sig to the list. The problem with this approach is that there is no obvious way to identify
the Ricardian hash. This might bring into light the limits of the one-sig approach from the
original Ricardian issuance contracts. It suggests we need a wide protocol around the
notions of hash-then-sign and sign-then-hash.
-->

* SIG =
