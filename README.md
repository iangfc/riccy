# 'new gen' riccy v0.2

This file is a test bed for some ideas I have.  It is a Ricardian contract (or it will be when slight munging is done and the gods of financial cryptography smile) that implements certain ideas, and the discovery of these is also the content of the contract.

## TERMS

YOU are a holder of a unit of this instrument as issued on a digital rights system (eg a blockchain).

**RicardianHash.** The Ricardian Hash is the hash of this very document,
which is calculated over the raw markdown using a standard hash algorithm (pending).
I had tried to use the hash in git itself but that is unprovable unless the program has git
incorporated inside it, which is too high a burden.  Oh well, back to the old method.
Perhaps the Riccy hash can be attached as tag to the relevent version in git(hub)?
**

Note that additional Terms are defined in Parameters below.

## CONDITIONS

Because it is a contract, I have to offer something to you, the reader and holder of some instrument that you might have acquired.

That offer is this:

I, being {{ISSUER}}, the issuer of this contract, _offer_ YOU an irrevocable grant of a one-person non-unique transferable licence to use and enjoy the ideas within this document.

Now, also because this is a contract, you should both _accept_ and _provide good consideration_ for this above right, so that we establish a contract between us as parties.  Therefore:

I {{ISSUER}} require you to send, and you agree to send {{PRICE}} sats (or as many as fees, good graces and general happiness inspire you) to {{BSV_address}} on the BSV network, citing the Ricardian Hash of this contract.  The act of sending is your _acceptance_ and the sats are good consideration.  Fame and fortune to follow.

Note that this is a pretty soft contract, as it's really here for _demonstration purposes_ as to what a contract is.  Also the LICENCE.md file somewhere nearby provides additional possibilities.  Also, it's all *AS IS* and dispute resolution guarantees happy outcomes.

## SOME PARAMETERS

Because I'm trialling a few different ideas here, I need some params:

* ISSUER = iangfc     # note this applies to where this file is stored and to the paymail below, fwiw
* PRICE = 100
* BSV_address = 1Mi2Hha5QM1zXD2tjJUv9carJis5zrStXz
* PAYMAIL = iangfc@centbee.com

Now, in extremely simple terms, this is a *program readable* Ricardian Contract with params laid out in the above format;  where that parameter is now used to set any variable found elsewhere using the moustache or double curly convention.

The rest of the document other than the parameters above is done in GitHub Flavoured Markdown Format.
Hopefully there is no clash in semantics.
The combined format might be Ricardian Topping on GitHub Flavoured Markdown Format.

## FORMAT

    * Task = move this to its own document.

This format for Ricardian contracts is compatible with and layered over the [GitHub Flavoured Markdown Spec](  https://github.github.com/gfm/ ) for the simple reason that part of this project is to experiment with the use of github editing as a collaboration tool.

### Parameters

For sake of argument we will specify:  any line with a star, then a single (program language style) word to left, an equals symbol, and whatever comes after that until end of line or a comment symbol led by a hash.

####EBNF

Or in EBNF if I can recall my crusty CS:

    Parameter = "*", identifier , "=", value [ "#" , text ], "\n" ;

    Parameter = "*", identifier, [.], "*", [lines], "**", "\n" ;

    lines = [words], "\n" ;

    Variable = "{{", Parameter, "}}" ;

    Identifier = firstletter, [letters], lastletter

    firstletter = [a-zA-Z_]

    letter = firstletter | [-0-9]

    lastletter = firstletter | [0-9]

Params come in two forms, as a specific one line assignment using star lists:

 * Tag =  some value words.
 * which can be intermingled as a list, or
 * Tag2 = can have some more value words.
 * Tag3 += and also an array or multivalue form,
 * Tag3 += which is useful for routing to URLs that are replicated.
 * Note that the tags are one word each constructed of [a-zA-Z0-9_-] and are case insensitive.
 * Dashes and underscores cannot lead or end, as this interferes with emphasis.

### Multiline tagged paragraphs

*Multiline* A paragrah can be tagged as a multiline,
which starts with an emphasised tag word, in this case
the word Multiline.
It is permitted to have a single fullstop directly after the tag word, like *WithFullstop.*

Following the tag line is any number of lines of text, including paragraphs and empty lines.

The multiline format is always closed by
  + a new section,
  + the end of file, or
  + two or more stars on its own line followed by an empty line or other block closer, as follows this very line.
Sadly, when markdown renders its formatting on double-star, it folds all these lines into one para, so it ends up on the end of line, not the next line.  No matter, *remember* to place the double-star on its own line in the raw text:
**

*Closed.*  See! In the Ricardian, the above is now closed and a new one is opened, called Closed.
It has to have the closing marker by itself on its own line to avoid the
Ricardian parser doing strange things.  Another way to close it is to use three or more stars:
***

Which should trigger a line in HTML.  Let's see.

***Emphasis*** Also note that more emphasis is allowed for the
open of a multiline, as long as it is a legal set using only star, and not underscore.
That's because it is a common pattern in coding to use underscores inside names, like _thing.
This should be done carefully by the author as the Markdown parser sees underscores as emphasis_.

****

The Multiline hasn't been used much in the past, but there are certain key elements in contracts that need it.

### Headings

Headings should be in strict ATX format, that is as above with leading hashes. SETEXT headings are not supported (those with a line underneath) which is to say they are ignored by the Ricardian parser.

The Ricardian must start with a single one-hash non-empty heading as the first line (after empties).  This is needed to signal the start of hashing.

0-3 spaces leading is OK, more will cancel the heading (TBD). Always one space after the leading hashes (TBD). Optional hashes after a space are stripped (TBD).

### End

The Ricardian is ended by the single paramater SIG being the signature of the contract.  It can be empty, although what this means to higher layer code is undefined.  NB, as with the first heading, this defines the end of hashing.

### Comments

 - I was trying to establish a convention that Markdown lists that start with hyphens, like this one,
 - are to be treated as comments for the purpose of contracts.
 + This is not a normal legal convention but I have found that comments are very useful;
 + this may reflect a different mindset coming from a CS background, where we comment our code!
 * The meaning of comments is ultimately found in dispute resolution, but
 * the suggestion herein is that they are not a legally binding part of the contract.
 - Unfortunately it's screwed up bc all the lists look the same!?!!?!  This may be ***_DOA_***.

OK, how about the HTML comment?

<!-- this is a comment -->
And <!-- this is a multiline
comment that doesn't end until --> it ends.

## LEGAL

**Dispute_Resulution.**  All disputes will be resolved by rolling fair dice at a beach bar of my choice, loser to pay the next round.

## OMISSIONS

For various reasons which I won't explain today, I am leaving some stuff out:
* _my issuer signature_ which is to say, this document does not have a single observable token within it that could be interpreted as a signature by me making it a good offer, and nor does it have my public key.
* _routing_ to a payment system, as this is hard coded above for ease of experiment.
* tight specification of Markdown, check out the  [GitHub Flavoured Markdown Spec](  https://github.github.com/gfm/ ).
* compliance with EBNF which you can read about on wikipedia.  Expect less.  Oops, I forgot whitespace.

These are left as exercise to the reader, um, counterparty.

## END

Anything not included above is missing.  File a dispute.  Find my beach bar, bring dice and money.

SIG =
