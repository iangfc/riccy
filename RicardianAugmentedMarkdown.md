
# Ricardian Augmented Markdown

 * Version = 2.1.0 of this document.  RAM itself is Version 2.
 + let's call the Ini format Version 1.

This format for Ricardian contracts is compatible with and layered over the
[GitHub Flavoured Markdown Spec](https://github.github.com/gfm/).
Part of this project is to experiment with the use of github editing
as a collaboration tool for programmers to write Ricardian contracts,
so it is natural to rely on that specification; other
[Markdowns](https://commonmark.org/) have not been considered but there is
no known reason why they wouldn't work.

The format - RicardianAugmentedMarkdown or RAM for now -
is designed to allow a simple line-based parser to extract
what it needs and not require complicated processing typical of sophisticated grammars.
Note that the RAM layer sees through or ignores most of the Markdown formatting,
as extraction not formatting is it's job.

A companion document ['new gen' riccy v1.0](https://github.com/iangfc/riccy) introduces the topic
more gently.

## Parameters

There are three parameter forms:  Singletons, Arrays, and Multilines.

### Tag-value Parameters (Singletons and Arrays)
Example:
 * singleton = star - space - tag - equals - content
 * array += star ... duplicated many times

A basic parameter is a line with
 + a star (bullet list item, and no other bullet such as plus or dot),
 + a single (program language style) tag name,
 + an assignment symbol, which can be one of:
     + equals symbol = or,
     + a plus-equals symbol +=, and
     + mixing them is undefined
 + whatever comes after that until end of line (or a comment starts).
 + plus and dash bullet points are ignored in RAM.

The presence of = or += in a star bullet list is a trigger, and has to be formatted correctly with at least a space between the bullet and tag, and a space between the tag and the symbol. No spaces are needed after the symbol, and if there is no value, then then any spaces will be stripped anyway by canonicalisation.

Tag-Value Params come in two forms.
_Firstly and secondly_ as a specific one line assignment using star bullet lists.
  + _First_, if = is used, it signals a _singleton_ or singular value, and cannot be repeated.
  + _Second_ if += is used, this becomes an array of values, and by adding more with that tag,
more values are added.
  + if = and += are mixed with the same tag, the result is undefined. It is best if the reader triggers an error on this condition.

Otherwise, the rules are the same for each of these two forms:

 * Tag = some value words, until eoln.
     + which bullets can be intermingled inside a list...
 * TAG_2 = can have some more value words.
 + The _second form_ is the array form:
 * Tag-3.array += iang.org
     + Using += signals that this Tag-3 has an _array_ or multivalue form,
 * Tag-3.array += github.com
     + which is useful for (eg) routing to URLs that are replicated.
 * Tag.4.singleton = You can mix = or += symbols in the content, the first one counts.
 * Whitespace = you must have at least a space after the star bullet and before the symbol
     + after the symbol is optional because canonicalisation will trim an empty value back to the symbol

### Rules for Tag Names
The above shows several legal tags in legal parameters. The rules for tag naming are similar to programming languages:

 + Tags start with an alpha [a-zA-Z].
 + Tags end with an alphanumeric [a-zA-Z0-9].
 + Tags contain also
     + numerals (not in first character) and
     + three symbols being hyphens, fullstops and underscores [a-zA-Z0-9_-.] (not in first or last character). The three symbols are equivalent.
 + Tags are Case Sensitive;
     + "Oh, East is East, and west is west, and never the twain shall meet."
     + Devs are familiar with this concept, and I am
       [reliably informed](https://twitter.com/CommonAccord/status/1421570064206090242)
       that lawyers are careful too.
     + NB - under revision - we may switch to case InSensitive.
 + Be careful with underscores in the tag name as they can also be interpreted as emphasis by markdown.

Illegal tags would include 1bad, -bad, bad#tag, .bad or bad_ or bad= .  XXX Don't duplicate the punctuation, as that will likely be enforced as bad: dupli__cated..punct-._ation would be bad.

### Multiline Tagged Paragraphs

*Multiline* A paragrah can be tagged as a multiline,
which starts with an emphasised tag word, in this case
the tag Multiline will have these 3 lines.

*Closure* Following the tag line is any number of lines of text,
including paragraphs, comments and empty lines.
The multiline format is always closed by
  + a new section, such as the section '### Multiline' above, or
  + two or more stars on its own line, as follows this very multiline.
  + The start of a new multiline definition.
Sadly, when markdown renders its formatting on double-star,
it folds all these lines into one para,
so it ends up displayed on the end of line, not the next line.
No matter, _remember_ to place the double-star on its own line in the raw text:
**

*Closed.*  See! In the Ricardian, the above is now closed and a new multiline is opened,
this time called Closed.
It has to have the closing marker by itself on its own line to make it simpler for the
Ricardian parser to handle without inordinate complexity.
Another way to close it is to use more stars than two:
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
but there are certain key technical elements in contracts that need it such as keys.
(Watch this multiline be terminated by the following section 'Comments'.)

## Comments
HTML comments \<!-- like this one --> are implemented in a partial form:
 
 - no comments before start or after SIG/end, nor on the 1st heading line nor on the last SIG line.
 - only one comment participant (pair or begin or end) per line
 - any parameters inside comments MUST be ignored
 - mixing comments with the start of a multiline is verbotten! as a simple line-based parser cannot cope with two multi-line things going on at once.

Hence the following are legal:
  + \<!-- this is a comment -->
  + \<!-- this is a multiline
    comment that doesn't end until it ends: -->

Whereas these are not legal:
  - \<!-- one --> and \<!-- two --> multiple comments on one line
  - \<!-- starts on one line
  - ends on this line --> but \<!-- starts again on the same line
  - before ending! --> and vice versa
  - \<!-- a comment with a comment start in it: \<!-- -->
  - any text with an unopened comment --> ending in it
  - \# First Line Intro \<!-- with an illegal comment -->
  - end of file without closing the comment, as this will hide the SIG
  * SIG = ThisIsMyArmouredSignature \<!-- this is an illegal comment -->

NB1. Comments are not a normal legal convention but I have found that comments are very useful;
this may reflect a different mindset coming from a CS background, where we comment our code!
The meaning of comments is ultimately found in dispute resolution, but
the suggestion herein is that they are not a legally binding part of the contract.
For this reason, it is useful for the comment to be treated as 'softer' by the markdown
display engine (but not disappeared, please!)

\<!-- NB2: Comments of the HTML form are much harder because they can cross lines,
and we do not want to impose a DOM model
nor a look-ahead parser on the coder, hence there are the above limitations
to make it easier for a simple line based parser.
It would be far better if we could use line-based comments as with computer languages
such as // in Java but I can see no way to do that in Markdown :-( . -->

## Headings
Headings are for the reader, not the parser in general.

### Formats
Headings should be in strict ATX format, that is as above with leading hashes.
SETEXT headings are not supported (those with a --- line underneath)
which is to say they are ignored by the Ricardian parser.
The only import of this is that the Primary Heading (below) must be a single hash heading.

<!--
### (TBD) Heading Tags
I like the idea of automatically tagging the headings with eg 1.2 or 3.4.
But is it worth it to do such complications?

Another possibility is to insert tag names into the headings, as with the multiline paragraph.
-->

## Details

### Whitespace
Only spaces should be used where whitespace is indicated, such as surrounding the tag in a parameter.

### Canonicalisation
In order to assist repeatable hashing so that the document has one clear message digest as an identifier,
the document is canonicalised before hashing and before signing.
Canonicalisation consists of these rules:
 1. All empty lines before the primary header and after the signature trailer are removed.
 2. All whitespace including end of line characters is removed from the end of every line.
 3. Every line has a *nix* newline '\n' character (0x0a) added to it.

Note that this differs from previous rules in a couple of ways.
Firstly, prior generations used MS end of line "\r\n" as the hashing line terminator.
But MS tools don't surface that ending any more whereas the '\n' ending
whereas text formatted documents are still prevalent in Linux/Mac/Unix platforms.
Secondly, every line gets a line ending, unlike (Open)PGP which dropped the last line ending.
Having a separate rule for the last line is just a nuisance to the coder.

### UTF
No UTF supported as yet (TBD). It should work...???

### EBNF

Or in EBNF if I can recall my crusty CS:


    Parameter = "*", identifier , "=", value [ "#" , text ], "\n" ;

    Parameter = "*", identifier, [.], "*", [lines], "**", "\n" ;

    lines = [words], "\n" ;

    Variable = "{{", Parameter, "}}" ;

    Identifier = firstletter, [letters], lastletter

    firstletter = [a-zA-Z_]

    letter = firstletter | [-0-9]

    lastletter = firstletter | [0-9]

### It Begins and It Ends
Having a defined start and end makes it easy for line-based parsers to look
at what format a file might be in, and to define where hashing starts and stops.

### Start Heading
The Ricardian must start with a single one-hash non-empty heading as the first line
(after empty lines, which must be stripped out) as is shown at top of this file.
This first primary Heading is essential to signal that this is a RAM file
(as opposed to older generation 1 Ricardian contracts which started with 5 dashes)
and to initiate the start of hashing.

 + Reserved headings (first, Signatures and END)
   must have zero leading spaces. <!-- this is because parsing is much messier on these lines -->
 + With other general headings, 0-3 spaces leading is OK, more will cancel the heading in Markdown (TBD).
 + Always have at least one space after the leading hash(es) as required by Markdown.
 + Experimental - the title in the starting heading can be captured into a parameter 'TITLE' for convenience (TBD).
 + Optional trailing hashes after a space are stripped from the name/heading in formatting/presentation (TBD) as per Markdown.

### Reserved Words
The following cannot be used:
 - *TITLE* as a tag, reserved for the leading heading (TBD).
 - *Signatures* as a heading, except as the last heading to only include the signatures.
 - *SIG* as a tag, except within the Signature heading.
 - *HASH* as a tag, as that indicates an override canonical Ricardian message digest algorithm over the present document (TBD).
 - *RicardianHASH* as a tag, as that indicates an override canonical Ricardian message digest algorithm over the well formed contract (TBD).
 - *END* as a heading terminates the document for hashing purposes.

### WIP
This is a work in progress and will change as code gets developed and struggles against reality.

## The End is Nigh

The end block of a Ricardian contract consists of signatures and the END signal.

### The End is the END

For Ricardian hashing purposes, the heading END will always end the primary document:

 + This heading's hash will be hard-left, without spaces, and include only one space before
the END.
 + Any number of hashes are permitted, although 6 is generally a limit in formatting.
 + The heading itself is customarily in upper case, and lower case should
be avoided.
 + No comment or whitespace permitted after the heading.

### How Signatures are Formed
Signatures can be inside the hashed envelope or outside, that is, they can be
either before the END heading or after it.
When the Ricardian is an issued contract, it generally includes signatures 
by the issuer, and that signature is generally before the END block and counts
within the Ricardian Hash.

NB,
 + To make parsing easier there should be precisely one space before and after the bullet,
   and also before the assignment.
 + But, no space is necessary after the assignment as space-stripping makes that redundant.
 + As noted above, there cannot be any comment artifact on within, appended to a SIG line, nor interspersed within SIG lines.
 + The signature can be empty, and in particular this is what is set in the act or signing;
   what this means to higher layer code is undefined,
   but at least it can still be hashed.

### Multiple Signers in Counterparts (TBD)
The possibility of multiple signatures exist by using the += array parameter form
to get signatures over the document without the other signatures being part of that
body.
In the act of signing, each existing signature in the block is reduced to one line
being the empty signature:

 * sig +=

Hence, each signature is over the unsigned contract, and then each signature is
inserted into the block of signatures independently.

In the legal context, these signatures are in _counterparts_ form which means each
stands independent of each other, and a contract is formed from collecting all the
signed copies together.

<!-- 
One problem with this approach is that there is no obvious way to identify
how many signatures are the right number. Technically a new signer could
add their signature into the block, and it would be valid, except for the
small detail that the Ricardian hash will now change.
-->

### Multiple Signers in Serial (TBD, deferred)

Potentially we could also define signers in serial, in which the second signer
also signs over the first signature.
This could be done by duplicating the singleton form, but this is stretching things somewhat.
This entire possibility is deferred until useful.

### The END is here

And, because this is nominally a correct RAM file, here comes the ending SIG,
followed by the END signal.

## Signatures
 * SIG = ThisISaFAKEarmouredSIGNATURE
# END
