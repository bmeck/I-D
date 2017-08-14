---
title: .mjs File Extension for EcmaScript
abbrev:
docname: draft-bfarias-json-home-00
date: 2017
category: info

ipr:
area: General
workgroup:
keyword: Internet-Draft

stand_alone: no
pi: [toc, tocindent, sortrefs, symrefs, strict, compact, comments, inline]

author:
 -
    ins: B. Farias
    name: Bradley Farias
    organization:
    email: bradley.meck@gmail.com
    uri:

normative:
  RFC4329:
  RFC2119:

  ECMA-262:
    author:
      org: European Computer Manufacturers Association
    title: "Standard ECMA-262"
    date: August 2017
    target: http://www.ecma-international.org/publications/standards/Ecma-262-arch.htm

  TC39-MIME-ISSUE:
    author:
      org: TC39
    title: "Add `application/javascript+module` mime to remove ambiguity5"
    date: August 2017
    target: https://web.archive.org/web/20170814193912/https://github.com/tc39/ecma262/issues/322

--- abstract

This document proposes a new file extension be added to EcmaScript MIME types.

--- note_Note_to_Readers

The issues list for this draft can be found at <https://github.com/bfarias/I-D/labels/javascript-mjs>.

The most recent (often, unpublished) draft is at <https://github.com/bfarias/I-D/tree/master/javascript-mjs>.

Recent changes are listed at <https://github.com/bfarias/I-D/commits/master/javascript-mjs>.

--- middle

# Introduction

In the [ECMA-262] 6th Edition of the EcmaScript language standard a new top level grammar was introduced for EcmaScript Modules. This now makes two possible top level grammars for any given Source Text of EcmaScript. The TC39 standards body for EcmaScript has determined that Media Types are outside of their scope of work [TC39-MIME-ISSUE].

It is not possible to fully determine if a Source Text of EcmaScript is meant to be parsed in the Module or Script grammar goals based upon content alone. Therefore, scripting environments must use out of band information in order to determine what goal a Source Text should be treated as. To this end Node.js has chosen to adopt a new file extension of .mjs for determining the goal of a given Source Text.

The existing Media Type registration of {{RFC4329}} also has references to withdrawn standards and should be updated to reflect that as well.

## Notational Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT",
"RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in
{{RFC2119}}.

# Changes

This specification proposed to remove the text from {{RFC4329}} pertaining to outdated or withdrawn references to JS15, ECMA, EcmaCompact, and E4X.

It redefines the types in {{RFC4329}} to be relevant to any environment wishing to obtain Media Type information related to EcmaScript.

# IANA Considerations

## JavaScript Media Types

The Media Types are to be updated to remove withdrawn or out of date information. In addition, a new file extension of .mjs is to be added to the list of File extensions with the restriction that it must correspond to the Module grammar of [ECMA-262].

### text/javascript

Type name:               text
Subtype name:            javascript
Required parameters:     none
Optional parameters:     charset, see section 4.1.
Encoding considerations:
  The same as the considerations in section 3.1 of [RFC3023].

Security considerations: See section 5.
Interoperability considerations:
  None, except as noted in other sections of this document.

Published specification: [ECMA-262]
Applications which use this media type:
  Script interpreters as discussed in this document.

Additional information:

  Magic number(s):             n/a
  File extension(s):           .js, .mjs
  Macintosh File Type Code(s): TEXT

Person & email address to contact for further information:
  See Author's Address section.

Intended usage:          COMMON
Restrictions on usage:   .mjs must correspond to the Module grammar of [ECMA-262]
Author:                  See Author's Address section.
Change controller:       The IESG.

## application/javascript

7.2.  application/javascript

Type name:               application
Subtype name:            javascript
Required parameters:     none
Optional parameters:     charset, see section 4.1.
Encoding considerations:
  The same as the considerations in section 3.2 of [RFC3023].

Security considerations: See section 5.
Interoperability considerations:
  None, except as noted in other sections of this document.

Published specification: [ECMA-262]
Applications which use this media type:
  Script interpreters as discussed in this document.

Additional information:

  Magic number(s):             n/a
  File extension(s):           .js, .mjs
  Macintosh File Type Code(s): TEXT

Person & email address to contact for further information:
  See Author's Address section.

Intended usage:          COMMON
Restrictions on usage:   .mjs must correspond to the Module grammar of [ECMA-262]
Author:                  See Author's Address section.
Change controller:       The IESG.

--- back


# Acknowledgements

Thanks to Suresh Krishnan, Alexey Melnikov, Mark Nottingham, James Snell, Matthew A. Miller, and Allen Wirfs-Brock for guiding me through this process.
