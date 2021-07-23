# 'new gen' riccy v0.3

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
The combined format might be Ricardian Topping on GitHub Flavoured Markdown Format
or more simple
<a href="RicardianAugmentedFormat.md">Ricardian Augmented Format</a>.

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
