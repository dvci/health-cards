- Feature Name: `multipleHC-singleQR`
- Start Date: 2022-02-07
- Status: Draft for comment

# Summary

[summary]: #summary

There may be circumstances where an individual receives multiple SMART Health Cards. For example, if an individual may receive Health Cards from different issuers, and so these cards will have different payloads. In this case, it would be beneficial to have functionality in place for storing multiple SMART Health Cards into a single QR code, as long as the payload is small enough.

# Motivation

[motivation]: #motivation

Consolidating multiple SMART Health Cards into a single QR code would simplify the verification process, as the verifier will only need to scan a single QR code for verification. This feature would lessen the burden on the card holder, who will no longer need to keep track of multiple SMART Health Cards.

# Guide-level explanation

[guide-level-explanation]: #guide-level-explanation

For this situation, it is assumed that each Health Card's JWS payload has been minified and compressed, and each Health Card contains a signature.

To combine into a single QR code, the JWS strings can be concatenated together with a delimiter character. The delimiter character must be `base45` and `base64url` compatible. The colon (`:`) character is compatible with the `base45` alphabet and is a URL reservable character in the `base64url` alphabet, so it can be used as the delimiter character to distinguish the different JWS strings. After combining the signatures into a single JWS string, QR generation can proceed using the existing process, implementing chunking as needed.
