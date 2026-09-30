# 'new gen' riccy v1.0

This file is describes a 2nd Generation of Ricardian Contract based on Markdown format.  It is (also) a Ricardian contract so as to eat its own dog food.

It is more fully documented in
<a href="RicardianAugmentedMarkdown.md">Ricardian Augmented Markdown</a>.

## Constructs

In the Ricardian contract, there are 3 basic constructs, as shown in the examples below. Firstly,
 * Parameter = a parameter is a setting for programs and display browsers to interpret the contract.

Secondly,

**Named_Paragraph.** A paragraph (or more) can have a Parameter name attached to it as the first highlighted term, allowing programs or display browsers to interpret it with special care.
**

Thirdly, the construct {{HASH}} will cause the value set at that parameter name to be displayed by a contract browser.

These constructs are further explained below. Most everything else is standard Markdown.

## CONDITIONS

Because it is a contract, I have to offer something to you, the reader and holder of some instrument that you might have acquired, and I have to particularise the details.

### Clauses

That offer is this, in readable clauses:

*Offer.*  I, being {{ISSUER}}, the issuer of this contract, _offer_ YOU an irrevocable grant of a one-person non-unique non-transferable licence to use and enjoy the ideas within this document.

Now, also because this is a contract, you should both _accept_ and _provide good consideration_ (aka payment) for this above right, so that we establish a contract between us as parties.  Therefore:

  **Consideration** I {{ISSUER}} require you to send, and you agree to send {{PRICE}} sats (or as many as fees, good graces and general happiness inspire you) to {{BSV_address}} on the BSV network, citing the Ricardian Hash of this contract.  The act of sending is your _acceptance_ of the above _offer_, and the sats are good _consideration_.  Fame and fortune to follow.

Note that this contract is *AS IS* and dispute resolution guarantees happy outcomes.

<!--
This is a pretty soft contract, as it's really here for _demonstration purposes_ as to what a contract is.  Also the LICENCE.md file somewhere nearby might provide additional possibilities.
-->

### Parameterised Details

A Ricardian contract requires details to be readable, so I need some params:

* TYPE = licence       <!-- Which says that this is a Licence for some intellectual good -->
  - Contracts generally follow patterns, and type {{TYPE}} will be a signal to software as to how to interpret the details within the pattern.
* ISSUER = iang        <!-- note this describes the name of the person issuing, required for most contracts -->
  - For most contracts of issue, there will be a primary issuer. For contracts between parties, there might be PARTY and COUNTER_PARTY.

The following sub-elements are typically needed for a fuller contract of issuance
 * subtype = sale       <!-- Which suggests that the licence can also describe its own sale. -->
   - The subtype {{subtype}} can then go on to require these additional params:
 * chain = BSV          <!-- Important to not send value to the wrong chain/address formats -->
 * PRICE = 100
 * BSV_address = 1Mi2Hha5QM1zXD2tjJUv9carJis5zrStXz
 * PAYMAIL = iangfc@centbee.com

In extremely simple terms, this is a *program readable* Ricardian Contract with parameters laid out in the above format;  where that parameter is now used to hold any value that might be useful for the program or for the display.

## FORMAT

Now we explain the formats of all the above.

### Simple Parameters

 * name = value

Parameters are set as bullet points in Markdown format, and are otherwise unallocated. This allows us to extend the Markdown as above to define params roughly as ___star name equals value___ convention.

The value part must sit in the line to the right of the equals. And comment to the right is ignored.

The + and - bullet forms, also defined by Markdown for bullets, are ignored, and can be used for just bullet points.

#### Parameter controls

A parameter can also have controls set on it:
 - compulsory, which means that a contract is not valid unless it is filled in, either herein or in a primary contract that cites this one as its template.
 - type fields such as integer (0, positive, etc), decimal (number of decimal points), string, etc.

The formats for these controls haven't settled as yet. Here's some ideas:
 * obligatory_value =!       <!-- means, as it's empty, this must be supplied by referring contract-->
 * array += FirstValue       <!-- means that the parameter array can have many values, in an array -->
 * fixed_value == MustBeThis <!-- means that this paramameter cannot be overridden in a referring contract -->

#### Parameter Name Rules

The name of the parameter loosely follows some well-trodden computer science conventions:

 * Names start with a letter, and can include digits after the first letter.
 * Case = Uppercase and lowercase makes no difference <!-- Case is same as CASE as is case -->
    - ok, which is it? RAM says it is case insensitive! WIP.
 * Punctuation_marks = _,- <!-- Names can include these symbols only, they have no meaning, they are reduced to one generic symbol -->
 * Whitespace = none! <!-- So " * This Name = moo" is an invalid parameter -->

**Punctuation.** This is a bit tricky. The only marks of punctuation that are accepted within a name are underscore, dot and dash. They all mean the same thing, being a punctuation symbol, and are equivalent. Hence, {{Punk_d}} will find and show the same parameter as {{PUNK-D}} as also {{punk.D}}.

Mixing and doubling up of marks is not allowed (too messy to code). The marks can only appear inside the name, not at beginning nor end.

### Named Paragraphs

**Named Paragraphs**. Paragraphs can be given a parameter name by highlighting that name on the first line.
The highlighting must be the first element of the paragraph
and must be proper in that the start must match the end.
Only __stars__ may be used in the highlighting of the name.
**

**Termination.** A 'Paragraph' is actually a block of text
that may consist of many paragraphs (in this case, two).
It or they are terminated by a single ___star-star___ on a separate line
following the text, as above.
In display, the termination symbol will often appear at the end of the last line,
and the browser may soften it in some fashion.

If there is no terminating ___star-star___ below a paragraph,
the block continues until either a ___star-star___ is found,
or a heading starting with # symbols is found, or the file ends.
This block of two paragraphs is terminated by the following heading:

#### Paragraph Name Rules

** Name Rules For Paragraphs. ** The names follow the above Parameter rules, with the addition of these two additional rules:

 + Spaces are introduced as marks which are equivalent to other marks for parameter name purposes.
 + A final punctuation dot is allowed for readability, and is ignored in the parameter name.
 + Spaces before or after are stripped. Multiple spaces are not allowed.

### Displayed Variables

Parameters can be be interpreted within the text by the 
moustached or double-curly format. This means that when
a display browser sees {{TYPE}} in the text,
it can substitute the word 'licence'.
When we see {{Offer}} the entire paragraph behind that parameter can be written in.

This is a display issue.  After having parsed the paramaters so as to read their values,
a display engine has to then re-parse to replace all the params. The way in which this is
done is not tightly defined at this level.

For example, a term {{ISSUER}} may require a hover or a click to make the parameter setting appear, depending on the settings on the browser. The way a paragraph is rendered is browser-specific.

### Ricardian and other Hashes

As above, when a parameter that has been set is found in double curlies the parameter's value can be displayed by the browser. These ones are always live, if not always displayable:

**RicardianHash.** The {{RicardianHash}} is the message digest of the top referring contract,
which is calculated over the raw markdown of that contract, and cannot be shown absent of a
proper contract context.
**

**HASH.** The {{Hash}} is the message digest of a current document. For this present document it can be shown, and that is helpful for a later party to copy/paste the value into their contract, so as to include this document by hash reference as a template. (Herein, the hashmark or # is the heading indicator whereas the term 'hash' refers to a message digest code.)
**

When {{HASH}} appears in the text herein, it can always be displayed because the browser
will simply canulate the message digest of this document.
When {{RicardianHash}} appears, this is not displayable herein because the contract is incomplete; it lacks certain obligatory parameters that must be filled in by a referring contract.
**

### Reserved words / parameter names

These are the reserved words, which are not permitted for the author to use in any parameter setting construct.

 - RicardianHash refers to the message digest of a properly formed contract.
 - Hash is the message digest over this very document, assuming it is to be referred to by other documents.
 - MD is the message digest algorithm, if that is needed to reset the default.
 - Include sets a hash (or other unique value) that refers to a template document to be included within this document.
 - V is a version number. The values are reserved for the future, but likely look like: 1.2.3 .
 - END is not allowed for any heading (or parameter) as it ends the document.
 - SIG can only be used for signatures, within that section.
 - Signatures can only be used to head the signature section.
 - TITLE is reserved for the contents of the leading heading of one hashmark only.

## Markdown Formatting

Other than the names of the parameters (as above) the document is formatted according to
[GitHub Flavoured Markdown Spec](https://github.github.com/gfm/).
Markdown is basically a formatting concept only,
and hopefully there is minimal collision in semantics between the two formats.
The combined format might be called Ricardian Topping on GitHub Flavoured Markdown Format
or more simply,
<a href="RicardianAugmentedMarkdown.md">Ricardian Augmented Markdown</a>.

### Comments

We have discovered over time that good contracts have comments, as does good code.
Here, Markdown lets us down badly. There is no line-based comment capability!
The only hack is to drop down into HTML formatting (allowed in Markdown!) and use those comments:

<!--
  -- this is a HTML comment!
  -->
HTML comments have a lot of drawbacks - token-based meaning horrible to code, clunky, etc - so to regulate them, we set some extra rules for good contracts:
 - No line can have more than one comment.
 - Multi-line comments can only have comment material in it.
 - A comment can not have anything after it closes. <!-- ie, this is the end: -->
These rules go some way to keeping the Ricardian format as line-based, which is essential to reduce the coding burden to something like a journeyman task. Life would be much better if there was an end-of-line comment format such as // in programming.

Comments are not part of the contract. They are documentation, explanation and indication of thinking. This is extremely valuable when your counterparty is your partner in business. Less valuable when your counterparty is your victim. Think contributive versus adversarial.

## Omissions

For various reasons which I won't explain today, I am leaving some stuff out:
  * _routing_ to a payment system, as this is hard coded above for ease of experiment.
  * how the _hashes_ are calculated.
  * how to sign over previous signatures, such as with witnessing.
  * Heading titles as parameters.

These are subject of a higher level, and are left as exercise to the reader, um counterparty, um developer.

## LEGAL

**Dispute_Resolution.**  All disputes will be resolved by rolling fair dice at a beach bar of my choice, loser to pay the next round.

### Signatures <!-- Part 1 the internal signatures -->

By convention only, any signatures are collected under a heading Signatures.

Each individual signature is recorded in an (array) parameter of name Sig:

 * Sig = 8d5859f6e6d66ddc24501b4ac1da2b3f7cb93e04
The above single signature itself is computed over the document until and including the heading END below, with the value set to empty (no space after the equals).

If additional signatures are to be included, use the += form in one sequential block, and set all precceding ones to ONE SINGLE EMPTY param with += so that they all sign over the same document and signing hash. This is known as signing in counter-parts in legal terminology.

The contract cannot be considered complete until all signatures are so collected, so some text should be added to state who must be signing in the signature block.

### Now Cometh .. The End

The code calculates the {{HASH}} over the document from the first heading to the heading labelled simply as END, immediatly below. Everything before the first heading, and below the END heading, is chopped out of the Ricardian envelope.

## END

Anything not included above is missing.  File a dispute.  Find my beach bar, bring dice and money.

### Signatures <!-- Part 2 the external Signature section -->

External signatures can be added and encoded like this, being a final bullet point with tag name of SIG:
   * SIG = 8d5859f6e6d66ddc24501b4ac1da2b3f7cb93e04
These are not inside the Ricardian envelope and do not effect the Ricardian Hash.
