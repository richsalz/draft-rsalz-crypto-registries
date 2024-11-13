---
title: A Template for IANA Cryptographic Registries
abbrev: IANA Crypto Registries
docname: draft-rsalz-crypto-registries-latest
category: bcp
stream: IETF
v: 3

ipr: trust200902
area: "Security"
workgroup: TBD
keyword: Internet-Draft
venue:
  group: "SAAG"
  type: "Security Area"
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
  JOSEREG:
    title: "JSON Web Signature and Encryption Header Parameters"
    target: "https://www.iana.org/assignments/jose/jose.xhtml#web-signature-encryption-header-parameters"
  NTPREG:
    title: "Network Time Protocol (NTP) Parameters"
    target: "https://www.iana.org/assignments/ntp-parameters/ntp-parameters.xhtml#ntp-parameters-3"
  TLSREG:
    title: "TLS Cipher Suites"
    target: "https://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-4"


--- abstract

This document provides recommendations for how IETF Working Groups
should create IANA registries that are related to cryptographic
algorithms.
It is based on the lessons learned from the TLS registries over
the years.

--- middle

# Introduction

This document provides recommendations for how IETF Working Groups
should create IANA registries that are related to cryptographic
algorithms.
It is based on the lessons learned from the TLS registries over
the years as described in {{?RFC8447}} and {{?I-D.draft-ietf-tls-rfc8447bis}}.

The guidance here can be summarized as follows:

1. Each registry SHOULD be "Specification Required," as defined
in {{!RFC8126, Section 4.6}}.

1. If required by the "Value" format (see {{value-column}}), consider reserving
a section for Private or Experimental Use.

1. Each registry SHOULD have a "Recommended" column (see {{recommended-column}}).

1. Each registry SHOULD have a "Comments" column (see {{comments-column}}).

1. Most registries will need additional columns.

# Terminology

{::boilerplate bcp14-tagged}

# Specification Required {#spec-required}

The intent of the Specification Required standard for cryptographic code points
is to allow for relatively easy registration of code points associated with
protocols and algorithms that are being developed outside of
IETF or IRTF. A key requirement is that the specification of the semantics
must be "permanent and readily available" as described
in {{RFC8126, Section 4.6}}.
The defining document should make explicit if Internet-Draft
documents qualify, as Section 4.6 does not say.
Authors of the defining document should read the entire {{RFC8126}}
and make sure their descriptions and requirements are clear.

Note that the IESG picks the Designated Experts, so they should not be named
in the defining document. Instead, specify the number of experts and how many
are required to approve.  Phrases like "one of two" or "two of three" are
common requirements for approval.  The defining document SHOULD NOT suggest
one person, to avoid a single point of failure.

Designated experts ensure the specification is publicly available.  They may
provide more in-depth reviews.  Their review should not be taken as an
endorsement of the new registry entry.

When the work is done by an IETF WG or IRTF RG, that group should
collaborate with the defining WG in order to provide appropriate review.
A WG that defines a cryptographic registry MAY wish to include text like
the following in its instructions to the experts to enforce this
behavior.  Such instructions should appear in the defining document.

DE Instructions
: Unless the WG chairs indicate otherwise via email, the Designated Experts
should decline code point registrations for documents which have already been
adopted or are being proposed for adoption by IETF working groups or IRTF
research groups.

# Suggested Columns

Here is a summary of the recommendation; each column is described in its
own sub-section below. The following paragraph can be used as a
template when defining a registry.

The columns are defined as follows:

- Value (required):  The value that appears in the data structure or protocol.
Additional sentences that describe the format, such as fixed-number of
bytes, text string, etc., should be added.

- Description (required): A brief desription, often pointing to a section
in the defining Reference.

- Reference (required): The publication defining the entry.

- Recommended (required): Whether or not this value is recommended for
general use.

- Comments (optional): Text that may be added to explain transitions,
or similar useful information.

## The "Value" column {#value-column}

The "Value" column is the identifier for the cryptographic items in the
registry. Every value SHOULD be unique within the registry.  Values
SHOULD ONLYy be re-used because of earlier mistakes and if they still
guarantee there is little to no chance of confusion.

Sometimes values are inherently unique. Example of this include ISO
Object Identifiers, and string identifiers like those in OpenSSH that
allow an identifier to have an "@domain-name" appended.  It is up to the
Working Group to decide if such values should be in a registry. Values
that would have a Recommended value of "Y" probably SHOULD appear.

In some registries, such as TLS Cipher Suites {{TLSREG}}, the values are
one or more bytes, while NTP uses a single multi-byte value, while JOSE
uses short text names ({{JOSEREG}}), such as "s5c" for an X.509
certificate chain.

If a name is not inherently unique, the defining WG MAY wish to set
aside a specific range or values for "Experimental or Private Use." It
does not seem necessary to separate "Experimental" from the "Private
Use" concept.  An example of private string identifiers from
{{!RFC6838, Sections 3.2 and 3.4}} are the prefixes "vnd." and "x.",
respectively.

Another reason for reserved values is for "greasing" the protocol,
to help prevent ossification by nework devices that do not allow
protocols to grow and evolve. See {{?RFC8701}} for more information.
Such entries are often makred as "Reserved" in their Description, and
a reference to "RFC8710" in their reference.

## The "Description" colummn {#description-column}

The "Description" is a brief description of the item.
In many cases, it will be a short reminder text that should serve
as a "guidepost" to the reference documentation, as done with the
NTP Extension Field Types in the NTP Registries, {{NTPREG}}.

## The "Reference" column {#reference-column}

For work done in the IETF or IRTF, the "Reference" entry will almost
always point to a RFC about to be published.
For work done outside these organizations, the reference should be
a URL that the Designated Experts have verified to meet the requirements
of {{spec-required}}.

## The "Recommended" column {#recommended-column}

This document specifies that a "Recommended" column be defined, with
three values that correspond to yes, no, and no opinion.  Specifying an
initial value of "Y" or "D" in this column MUST require Standards Action
{{!RFC8126}} for the defining RFC, otherwise the the field MUST be empty
or have the value of "N".
Not all
items defined in Standards Track RFCs need to be set to "Y" or "D".

The entry SHOULD also be left blank for values that are unassigned or
reserved.

Y
: Indicates that the IETF has consensus that the item is RECOMMENDED. This
only means that the associated mechanism is fit for the purpose for which it
was defined.  Careful reading of the documentation for the mechanism is
necessary to understand the applicability of that mechanism.  When the IETF
recommends mechanisms that have limited applicability, the working SHOULD
provide applicability statements that describe any limitations of the
mechanism or necessary constraints on its use.

D
: Indicates that the item is discouraged. This marking could be used
to identify mechanisms that might result in problems if they are used,
such as a weak cryptographic algorithm or a mechanism that might cause
interoperability problems in deployment. Implementers SHOULD consult the
linked references associated with the item to determine the conditions
under which it SHOULD NOT or MUST NOT be used.

N
: Indicates that the item has not been evaluated by the IETF and that
the IETF has made no statement about the suitability of the associated
mechanism. This does not necessarily mean that the mechanism is flawed,
only that no consensus exists.  The IETF might have consensus to leave
an items marked as "N" on the basis of it having limited applicability
or usage constraints.

Once an entry is created, there are specific requirements to change
the value. Cryptographic algorithms become weaker over time, as more
attacks on them are defined.
Any state transition to or from a "Y" or "D" value requires IESG Approval.

The following is text that can be used in the notes section of
any registry that has a "Recommended" column:

Note
: If the "Recommended" column is set to "N", it does not necessarily mean
that it is flawed; but rather that the item either has not
been through the IETF consensus process, has limited applicability, or
is intended only for specific use cases.  If the "Recommended" column
is set to "D" the item is discouraged and SHOULD NOT or MUST NOT be used.
Defining a "Recommended" column value to "Y" or "D" requires Standards
Action [RFC8126]. Any state transition to or from a "Y" or "D"
value requires IESG Approval.

## The "Comments" Column {#comments-column}

This is a brief free-text column that can be used to describe
transitions or limits on usage.
Examples include:

- Obsoleted by RFC xxx
- Only for TLS 1.3 or later

# Security Considerations

Using Specification Required rather than IETF Review does, admittedly,
lower the theoretical amount of review provided by a WG.  Experience has
shown, however, that WG members generally provided no cryptographic
review, especially in the case of referring to national cipher suites.

Recommended algorithms are regarded as secure for general use at the time of
registration, Over time, however, cryptographic algorithms and parameters
will be broken or weakened.  It is possible that the "Recommended" status in
the registry lags behind the most recent advances in cryptanalysis.
Implementers and users need to check that the cryptographic algorithms listed
continue to provide the expected level of security.

# IANA Considerations

This document is entirely about best practices for IANA-maintained
cryptographic registries.
It does not define any new registries but provides guidance to
those who need to do so.

--- back
