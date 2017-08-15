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
  RFC3023:

  ECMA-262:
    author:
      org: Ecma International
    title: "Standard ECMA-262: ECMAScript Language Specification"
    date: August 2017
    target: http://www.ecma-international.org/publications/standards/Ecma-262.htm

  TC39-MIME-ISSUE:
    author:
      org: TC39
    title: "Add `application/javascript+module` mime to remove ambiguity5"
    date: August 2017
    target: https://web.archive.org/web/20170814193912/https://github.com/tc39/ecma262/issues/322

  HTML:
    author:
      org: WHATWG
    title: HTML Living Standard
    date: August 2017
    target: https://html.spec.whatwg.org/multipage/scripting.html#prepare-a-script

--- abstract

This document proposes a new file extension be added to EcmaScript MIME types.

--- note_Note_to_Readers

The issues list for this draft can be found at <https://github.com/bfarias/I-D/labels/javascript-mjs>.

The most recent (often, unpublished) draft is at <https://github.com/bfarias/I-D/tree/master/javascript-mjs>.

Recent changes are listed at <https://github.com/bfarias/I-D/commits/master/javascript-mjs>.

--- middle


# Introduction

This document updates existing media types for the ECMAScript programming language. It supercedes the media types in [RFC4329].


# Background

In order to formalize support for modular programs [ECMA-262] now defines two top-level goal symbols for the ECMAScript grammar. This means that (in the absence of additional information) there are two possible interpretations for any given ECMAScript Source Text. The TC39 standards body for ECMAScript has determined that media types are outside of their scope of work [TC39-MIME-ISSUE].

It is not possible to fully determine if a Source Text of ECMAScript is meant to be parsed in the Module or Script grammar goals based upon content alone. Therefore, scripting environments must use out of band information in order to determine what goal a Source Text should be treated as. To this end some scripting environments have chosen to adopt a new file extension of .mjs for determining the goal of a given Source Text.


# Notational Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT",
"RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in
{{RFC2119}}.


# Registration

The ECMAScript media types are to be updated to point to a non-vendor specific standard undated specification of ECMAScript. In addition, a new file extension of .mjs is to be added to the list of file extensions with the restriction that it must correspond to the Module grammar of [ECMA-262]. Finally, the [HTML] specification is using text/javascript as the default media type of EcmaScript when preparing script tags; therefore, text/javascript has been moved intended usage from OBSOLETE to COMMON.


## text/javascript

Type name:               text
Subtype name:            javascript
Required parameters:     none
Optional parameters:     charset, see section 4.1 of [RFC4329].
Encoding considerations:
  The same as the considerations in section 3.1 of [RFC3023].

Security considerations: See section 5 of [RFC4329].
Interoperability considerations:
  See notes in various sections of [RFC4329].
  This media type does not specify the grammar of [ECMA-262] used.

Published specification: [ECMA-262]
Applications which use this media type:
  Script interpreters as discussed in [RFC4329].

Additional information:

  Magic number(s):             n/a
  File extension(s):           .js, .mjs
  Macintosh File Type Code(s): TEXT

Person & email address to contact for further information:
  See Author's Address section.

Intended usage:          COMMON
Restrictions on usage:   The file extension .mjs must be parsed using the Module grammar of [ECMA-262]
Author:                  See Author's Address section.
Change controller:       The IESG.


## application/javascript

Type name:               application
Subtype name:            javascript
Required parameters:     none
Optional parameters:     charset, see section 4.1 of [RFC4329].
Encoding considerations:
  The same as the considerations in section 3.2 of [RFC3023].

Security considerations: See section 5 of [RFC4329].
Interoperability considerations:
  See notes in various sections of [RFC4329].
  This media type does not specify the grammar of [ECMA-262] used.

Published specification: [ECMA-262]
Applications which use this media type:
  Script interpreters as discussed in [RFC4329].

Additional information:

  Magic number(s):             n/a
  File extension(s):           .js, .mjs
  Macintosh File Type Code(s): TEXT

Person & email address to contact for further information:
  See Author's Address section.

Intended usage:          COMMON
Restrictions on usage:   The file extension .mjs must be parsed using the Module grammar of [ECMA-262]
Author:                  See Author's Address section.
Change controller:       The IESG.

--- back


# Acknowledgements

Thanks to Suresh Krishnan, Alexey Melnikov, Mark Nottingham, James Snell, Matthew A. Miller, Adam Roach, and Allen Wirfs-Brock for guiding me through this process.
