---
title: A Template for IANA Cryptographic Registries
abbrev: IANA Crypto Registries
docname: draft-rsalz-crypto-registries-latest
category: bcp
v: 3

ipr: trust200902
area: "Security"
workgroup: TBD
keyword: Internet-Draft
venue:
  group: "Transport Layer Security"
  type: "Working Group"
  mail: "saag@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/saag/"
  github: "rsalz/draft-rsalz-crypto-registries"

stand_alone: yes
smart_quotes: no
pi: [toc, sortrefs, symrefs]

author:
 -
    ins: R. Salz
    name: Rich Salz
    organization: Akamai Technologies
    email: rsalz@akamai.com

normative:

informative:

--- abstract

This document updates the changes to TLS and DTLS IANA registries
made in RFC 8447. It adds a new value "D" for discouraged
to the recommended column of the selected TLS registries and
adds a "Comments" column to all active registries.

--- middle

# Introduction

This document instructs IANA to make changes to a number of the IANA
registries related to Transport Layer Security (TLS) and Datagram
Transport Layer Security (DTLS). These changes update the changes made
in {{!RFC8447}}.

<aside markdown="block">
  NOTE for IANA: This document specifies changes to the registry to update
  the changes made in {{RFC8447}}.
</aside>

This specification updates the "Recommended" column in TLS
registries to define a third value "D" for items that are discouraged.

# Terminology

{::boilerplate bcp14-tagged}

# Adding "Recommended" Column

The instructions in this document update the Recommended column,
originally added in {{RFC8447}} to add a third value, "D",
indicating that a value is "Discouraged". The permitted values
are:

Y:
: Indicates that the IETF has consensus that the
    item is RECOMMENDED. This only means that the associated
    mechanism is fit for the purpose for which it was defined.
    Careful reading of the documentation for the mechanism is
    necessary to understand the applicability of that mechanism.
    The IETF could recommend mechanisms that have limited
    applicability, but will provide applicability statements that
    describe any limitations of the mechanism or necessary constraints
    on its use.

N:
: Indicates that the item has not been evaluated by
    the IETF and that the IETF has made no statement about the
    suitability of the associated mechanism. This does not necessarily
    mean that the mechanism is flawed, only that no consensus exists.
    The IETF might have consensus to leave an items marked as "N" on
    the basis of it having limited applicability or usage constraints.

D:
: Indicates that the item is discouraged. This marking could be used to identify
    mechanisms that might result in problems if they are used, such as
    a weak cryptographic algorithm or a mechanism that might cause
    interoperability problems in deployment. Implementers SHOULD
    consult the linked references associated with the item to
    determine the conditions under which it SHOULD NOT or MUST NOT be used.

Setting a value to "Y" or "D" in the "Recommended" column requires IETF Standards
Action {{!RFC8126}}.  Any state transition to or from a "Y" or "D" value requires
IESG Approval. Not all items defined in Standards Track RFCs need to be set
to "Y" or "D". Any item not otherwise specified is set to "N". The column is
blank for values that are unassigned or reserved unless specifically set.

## Recommended Note {#rec-note}

Existing registries have a note on the meaning of the recommended column. For the
registries discussed in the subsequent sections this note is updated
with a sentence describing the "D" vaue as follows:

Note:

: If "Recommended" column is set to "N", it does not necessarily mean
that it is flawed; rather, it indicates that the item either has not
been through the IETF consensus process, has limited applicability, or
is intended only for specific use cases.  If the "Recommended" column
is set to "D" the item is discouraged and SHOULD NOT or MUST NOT be used.

# TLS ExtensionType Values

In order to refect the changes in the Recommended column allocation,
IANA SHALL update the TLS ExtensionType Values registry as follows:

- Change the registration procedure to:

~~~
    Values with the first byte in the range 0-254 (decimal) are assigned
    via Specification Required [RFC8126].  Values with the first byte
    255 (decimal) are reserved for Private Use [RFC8126].  Setting a
    "Recommended" column value to "Y" or "D" requires Standards Action [RFC8126].
    Any state transition to or from a "Y" or "D" value requires
    IESG Approval.
~~~

- Add a reference to this document under the reference heading.

- Update the "Recommended" column with the changes as listed below.  Entries
  keep their existing "Y" and "N" entries except for the entries in following table.
  A reference to this document SHALL be added to these entries.

|Value | Extension                   | Recommended |
|:-----|:----------------------------|------------:|
|4  |truncated_hmac                  |         D |
...

- Update note on the recommended column with text in {{rec-note}}.



# TLS Cipher Suites Registry

Several categories of ciphersuites are discouraged for general use and
are maked as "D".

Ciphersuites that use NULL encryption do not provide the confidentiality
normally expected of TLS. Protocols and applications are often designed
to require confidentialy as a security property. These
ciphersuites MUST NOT be used in those cases.

Ciphersuites marked as EXPORT use weak ciphers and were deprecated in
TLS 1.1 {{!RFC4346}}.

Cipher suites maked as anon do not provide any authentication and are
vulnerable to man-in-the-middle attacks and are deprecated in TLS 1.1
{{!RFC4346}}.

RC4 is a weak cipher and is deprecated in {{!RFC7465}}.

DES and IDEA are not considered secure for general use and are deprecated
in {{!RFC5469}}.

In order to refect the changes in the Recommended column allocation,
IANA SHALL update the TLS ExtensionType Values registry as follows:

- Change the registration procedure to:

~~~
    Values with the first byte in the range 0-254 (decimal) are
    assigned via Specification Required [RFC8126].  Values with the
    first byte 255 (decimal) are reserved for Private Use [RFC8126].
    Setting a "Recommended" column value to "Y" or "D" requires Standards
    Action [RFC8126]. Any state transition to or from a "Y" or "D"
    value requires IESG Approval.
~~~

- Add a reference to this document under the reference heading.

- Update the "Recommended" column with the changes as listed below.  Entries
  keep their existing "Y" and "N" entries except for the entries in following table.
  A reference to this document SHALL be added to these entries. This document does not
  make any changes to the DTLS-OK column.

| Value | Cipher Suite Name                             | Recommeded |
|:------|:---------------------------------------------|-----------:|
| 0x00,0x01	| TLS_RSA_WITH_NULL_MD5             |   D  |
...


- Update note on the recommended column with text in {{rec-note}}.


# TLS Supported Groups

In order to refect the changes in the Recommended column allocation,
IANA SHALL update the TLS Supported Groups registry as follows:

- Update the registration policy to include:

~~~
    Setting a "Recommended" column value to "Y" or "D" requires Standards
    Action [RFC8126]. Any state transition to or from a "Y" or "D"
    value requires IESG Approval.
~~~

- Add a reference to this document under the reference heading.

- Update the "Recommended" column with the changes as listed below.  Entries
  keep their existing "Y" and "N" entries except for the entries in following table.
  A reference to this document SHALL be added to these entries.

| Value | Curve | Recommended |
|:-|:-|-:|
| 1 |sect163k1 | D |
...

- Update note on the recommended column with text in {{rec-note}}.

- Replace the registry range table note column for the 0-255, 512-65535
  range with "Unallocated".

# TLS Exporter Labels Registry

This document updates the registration procedure for the TLS Exporter
registry and updates the Recommended column allocation.
IANA SHALL update the TLS Exporter Labels Registry as follows:

- Change the registration procedure from Specification Required to
  Expert Review and update it to include:

~~~
    Setting a "Recommended" column value to "Y" or "D" requires Standards
    Action [RFC8126]. Any state transition to or from a "Y" or "D"
    value requires IESG Approval.
~~~

- Add a reference to this document under the reference heading.

- Entries keep their existing Recommended column "Y" and "N" entries

- Update note on the recommended column with text in {{rec-note}}.

- update the note on the role of the expert reviewer as follows.

Note:
: The role of the designated expert is described in {{RFC8447, Section 17}}.
Even though this registry does not require a specification, the
designated expert {{!RFC8126}} will strongly encourage registrants
to provide a link to a publicly available specification. An
Internet-Draft (that is posted and never published as an RFC)
or a document from another standards body, industry consortium,
university site, etc. are suitable for these purposes.
The expert may provide more in-depth reviews, but their approval
should not be taken as an endorsement of the exporter label.  The
expert also verifies that the label is a string consisting of
printable ASCII characters beginning with "EXPORTER".  IANA MUST
also verify that one label is not a prefix of any other label.
For example, labels "key" or "master secretary" are forbidden.


# TLS Certificate Types

In order to refect the changes in the Recommended column allocation,
IANA SHALL update the the TLS Certificate Types registry as follows:

- Change the registration procedure to:

~~~
    Values in the range 0-223 (decimal) are assigned via Specification
    Required [RFC8126]. Values in the range 224-255 (decimal) are
    reserved for Private Use [RFC8126]. Setting a "Recommended" column
    value to "Y" or "D" requires Standards
    Action [RFC8126]. Any state transition to or from a "Y" or "D"
    value requires IESG Approval.
~~~

- Add a reference to this document under the reference heading.

- Entries keep their existing Recommended column "Y" and "N" entries.

- Update note on the recommended column with text in {{rec-note}}.


# TLS HashAlgorithm Registry

Though TLS 1.0 and TLS 1.1 were deprecated {{!RFC8996}}, TLS 1.2 will
be in use for some time. In order to refect the changes in the Recommended
column allocation, IANA SHALL update the TLS HashAlgorithm Registry
registry as follows:

- Update the registration procedure to include:

~~~
    Setting a "Recommended" column value to "Y" or "D" requires Standards
    Action [RFC8126]. Any state transition to or from a "Y" or "D"
    value requires IESG Approval.
~~~

- Add a reference to this document under the reference heading.

- Update the TLS HashAlgorithm registry to add a "Recommended" column
  as follows:

| Value | Descsription | Recommended |
|:----  |:-------------|------------:|
| 0 | none | Y |
...

- Add note on the recommended column with text in {{rec-note}}.


# TLS SignatureAlgorithm registry

Though TLS 1.0 and TLS 1.1 were deprecated {{!RFC8996}}, TLS 1.2 will
be in use for some time. In order to refect the changes in the Recommended
column allocation, IANA SHALL update the TLS SignatureAlgorithm registry
registry as follows:

- Update the registration procedure to include:

~~~
    Setting a "Recommended" column value to "Y" or "D" requires Standards
    Action [RFC8126]. Any state transition to or from a "Y" or "D"
    value requires IESG Approval.
~~~

- Add a reference to this document under the reference heading.

- Update the TLS SignatureAlgorithm registry to add a "Recommended"
  column as follows:

|Value | Descsription | Recommended |
|:-----|:-------------|------------:|
| 0 | anonymous| N |
...

- Add note on the recommended column with text in {{rec-note}}.

# TLS ClientCertificateTypes registry

Though TLS 1.0 and TLS 1.1 were deprecated {{!RFC8996}}, TLS 1.2 will
be in use for some time. In order to refect the changes in the Recommended
column allocation, IANA SHALL update the  TLS ClientCertificateTypes
registry as follows:

- Update the registration procedure to include:

~~~
    Setting a "Recommended" column value to "Y" or "D" requires Standards
    Action [RFC8126]. Any state transition to or from a "Y" or "D"
    value requires IESG Approval.
~~~

- Add a reference to this document under the reference heading.

- Update the TLS ClientCertificateTypes registry to add a "Recommended"
column as follows:

| Value | Descsription | Recommended |
|:------|:-------------|------------:|
| 1 | rsa_sign | Y |
...

- Add note on the recommended column with text in {{rec-note}}.

# TLS PskKeyExchangeMode registry

In order to refect the changes in the Recommended column allocation,
IANA SHALL update the TLS PskKeyExchangeMode registry as follows:

- Update the registration procedure to include:

~~~
    Setting a "Recommended" column value to "Y" or "D" requires Standards
    Action [RFC8126]. Any state transition to or from a "Y" or "D"
    value requires IESG Approval.
~~~

- Add a reference to this document under the reference heading.

- Entries keep their existing recommended column "Y" and "N" entries.

- Update note on the recommended column with text in {{rec-note}}.

# TLS SignatureScheme registry

IANA is requested to add a reference to this document under the reference heading.

# Adding "Comment" Column

IANA is requested to add a "Comment" column to the following registries:

- TLS ExtensionType Values
- TLS Application-Layer Protocol Negotiation (ALPN) Protocol IDs
- TLS CachedInformationType Values
- TLS Certificate Compression Algorithm IDs
- TLS Cipher Suites
- TLS ContentType
- TLS EC Point Formats
- TLS EC Curve Types
- TLS Supplemental Data Formats (SupplementalDataType)
- TLS UserMappingType Values
- TLS Authorization Data Formats
- TLS Heartbeat Message Types
- TLS Heartbeat Modes
- TLS SignatureScheme
- TLS PskKeyExchangeMode
- TLS KDF Identifiers

This list of registries is all registries that do not already have a
"Comment" or "Notes" column or that were not orphaned by TLS 1.3.

# Expert Review of Current and Potential IETF and IRTF Documents

The intent of the Specification Required standard for TLS code points
is to allow for easy registration for code points associated with
protocols and algorithms that are not being actively developed inside
IETF or IRTF. When TLS-based technologies are being developed inside
the IRTF/IETF they should be done in coordination with the TLS WG in
order to provide appropriate review. For this reason, unless the TLS WG
chairs indicate otherwise via email, designated
experts should decline code point registrations for documents which
have already been adopted or are being proposed for adoption by IETF
working groups or IRTF research groups.


# Security Considerations

The change to Specification Required from IETF Review lowers the amount
of review provided by the WG for cipher suites and supported groups.
This change reflects reality in that the WG essentially provided no
cryptographic review of the cipher suites or supported groups.  This
was especially true of national cipher suites.

Recommended algorithms are regarded as secure for general use at the
time of registration; however, cryptographic algorithms and parameters
will be broken or weakened over time.  It is possible that the
"Recommended" status in the registry lags behind the most recent advances
in cryptanalysis.  Implementers and users need to check that the
cryptographic algorithms listed continue to provide the expected level
of security.

Designated experts ensure the specification is publicly available.  They may
provide more in-depth reviews.  Their review should not be taken as an
endorsement of the cipher suite, extension, supported group, etc.


# IANA Considerations

This document is entirely about changes to TLS-related IANA registries.


--- back
