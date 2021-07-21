# Ricardian Augmented Markdown

This format for Ricardian contracts is compatible with and layered over the
[GitHub Flavoured Markdown Spec](https://github.github.com/gfm/).
Part of this project is to experiment with the use of github editing
as a collaboration tool for programmers to write Ricardian contracts,
so it is natural to rely on that specification; but it is likely that
other Markdowns work as well.

The format is designed to allow a simple line-based parser to extract
what it needs and not require complicated processing typical of sophisticated grammars.

## Parameters
A basic parameter is a line with a star (bullet list item),
then a single (program language style) word to left,
an equals symbol,
and whatever comes after that until end of line or a comment symbol led by a hash.

Params come in two forms, as a specific one line assignment using star bullet lists:

 * Tag =  some value words.
 * which can be intermingled inside a list...
 * _Tag2 = can have some more value words.
 * The second form is the array form:
 * Tag-3 += Using += signals that this Tag3 has an array or multivalue form,
 * Tag-3 += which is useful for routing to URLs that are replicated.

The above shows three legal tags being tag, _TAG2 and Tag-3.

The rules for tag naming are similar to programming languages:
 * Tags start with an alpha or underscore [a-zA-Z_].
 * Tags contain also numerals and hyphens [a-zA-Z0-9_-] (just not in first character).
 * Tags are case insensitive, mostly so that there are no surprises in dispute resolution.
 * Be careful with underscores in the tag name as they can also be interpreted as emphasis.

Illegal tags would include 1bad, -bad and bad#tag.

### Multiline tagged paragraphs

*Multiline* A paragrah can be tagged as a multiline,
which starts with an emphasised tag word, in this case
the tag Multiline will have these 3 lines.

*Closure* Following the tag line is any number of lines of text, including paragraphs and empty lines.
The multiline format is always closed by
  + a new section,
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
That's because it is a common pattern in coding to use underscores inside names, like _thing.
This should be done carefully by the author as the Markdown parser sees underscores as emphasis_.
****
*FullStop.* You can also put a single fullstop at the end of the tag name for style.
This will be stripped off.

*Comments.* The Multiline hasn't been used much in the past,
but there are certain key elements in contracts that need it.

## (TBD) Comments

I was trying to establish a convention that Markdown lists that start with hyphens, like this one,
 - are to be treated as comments for the purpose of contracts.
Comments are not a normal legal convention but I have found that comments are very useful;
this may reflect a different mindset coming from a CS background, where we comment our code!
The meaning of comments is ultimately found in dispute resolution, but
the suggestion herein is that they are not a legally binding part of the contract.

 * Unfortunately...
 - it's screwed up bc all the lists look the same!?!!?!
 + This may be ***_DOA_***.

OK, how about the HTML comment?

<!-- this is a comment -->
And <!-- this is a multiline
comment that doesn't end until --> it ends.

These are handled appropriately by display engines but are harder for line based
parsers to handle.

## Headings

### Formats
Headings should be in strict ATX format, that is as above with leading hashes.
SETEXT headings are not supported (those with a line underneath)
which is to say they are ignored by the Ricardian parser.
The only import of this is that the Primary Heading (next) must be a single hash heading.

### Primary Heading
The Ricardian must start with a single one-hash non-empty heading as the first line (after empties).
This is needed to signal the start of hashing, and to make it easy for line-based parsers to look
at what format a file might be in.

0-3 spaces leading is OK, more will cancel the heading (TBD).
Always one space after the leading hashes (TBD).
Optional hashes after a space are stripped (TBD).

### (TBD) Heading Tags
I like the idea of automatically tagging the headings with eg 1.2 or 3.4.
But is it worth it to do such complications?

Another possibility is to insert tag names into the headings, as with the multiline paragraph.


##EBNF

Or in EBNF if I can recall my crusty CS:


    Parameter = "*", identifier , "=", value [ "#" , text ], "\n" ;

    Parameter = "*", identifier, [.], "*", [lines], "**", "\n" ;

    lines = [words], "\n" ;

    Variable = "{{", Parameter, "}}" ;

    Identifier = firstletter, [letters], lastletter

    firstletter = [a-zA-Z_]

    letter = firstletter | [-0-9]

    lastletter = firstletter | [0-9]

## End SIG

The Ricardian is ended by the single paramater SIG being the signature of the contract
by the issuer.
NB, as with the first heading, this defines the end of hashing.

It can be an empty signature; what this means to higher layer code is undefined,
but at least it can still be hashed.  This allows for unsigned inclusions such
as standard terms and conditions within some agreed context.

* SIG =
