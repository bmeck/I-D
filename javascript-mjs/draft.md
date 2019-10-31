---
title: ECMAScript Media Types Updates
abbrev:
docname: draft-ietf-dispatch-javascript-mjs-04
category: info

ipr:
area: ART
workgroup: DISPATCH
keyword: Internet-Draft
updates: 4329

stand_alone: no
pi: [toc, tocindent, sortrefs, symrefs, strict, compact, comments, inline]

author:
 -
    ins: M. Borins
    name: Myles Borins
    organization: Google
    email: mylesborins@google.com
 -
    ins: M. Bynens
    name: Mathias Bynens
    organization: Google
    email: mths@google.com
 -
    ins: M. Miller
    name: Matthew A. Miller
    organization: Mozilla
    email: linuxwolf+ietf@outer-planes.net
 -
    ins: B. Farias
    name: Bradley Farias
    organization:
    email: bradley.meck@gmail.com

normative:
  RFC4329:

  ECMA-262:
    author:
      org: Ecma International
    title: "Standard ECMA-262: ECMAScript Language Specification"
    date: August 2017
    target: https://ecma-international.org/publications/standards/Ecma-262.htm

informative:

  HTML:
    author:
      org: WHATWG
    title: HTML Living Standard
    date: August 2017
    target: https://html.spec.whatwg.org/multipage/scripting.html#prepare-a-script

  SPECTRE:
    author:
      -
        name: Paul Kocher
      -
        name: Anders Fogh
      -
        name: Daniel Gerkin
      -
        name: Daniel Gruss
      -
        name: Werner Haas
      -
        name: Mike Hamburg
      -
        name: Moritz Lipp
      -
        name: Stefan Mangard
      -
        name: Thomas Prescher
      -
        name: Michael Schwarz
      -
        name: Yuval Yarom

    title: "Spectre Attacks: Exploiting Speculative Execution"
    date: January 2018
    target: https://arxiv.org/abs/1801.01203

  TC39-MIME-ISSUE:
    author:
      org: TC39
    title: "Add `application/javascript+module` mime to remove ambiguity"
    date: August 2017
    target: https://web.archive.org/web/20170814193912/https://github.com/tc39/ecma262/issues/322


--- abstract

This document proposes updates to the ECMAScript media types, superseding the existing registrations for "application/javascript" and "text/javascript" by adding an additional extension and removing usage warnings.  This document updates RFC4329, "Scripting Media Types".

--- middle


# Introduction

This document updates the existing media types for the ECMAScript programming language. It supersedes the media types registrations in {{RFC4329}} for "application/javascript" and "text/javascript".

# Background

In order to formalize support for modular programs, {{ECMA-262}} (starting with 6th Edition) defines two top-level goal symbols (or roots to the abstract syntax tree) for the ECMAScript grammar: Module and Script. The Script goal represents the more stand-alone structure where the code executes in the global scope, while the Module goal represents the module system built into ECMAScript starting with 6th Edition.

This separation means that (in the absence of additional information) there are two possible interpretations for any given ECMAScript Source Text. The TC39 standards body for ECMAScript has determined that media types are outside of their scope of work {{TC39-MIME-ISSUE}}.

It is not possible to fully determine if a Source Text of ECMAScript is meant to be parsed in the Module or Script grammar goals based upon content alone. Therefore, scripting environments must use out of band information in order to determine what goal a Source Text should be treated as. To this end some scripting environments have chosen to adopt a new file extension of .mjs for determining the goal of a given Source Text.

# Security Considerations

Module scripts in ECMAScript can request the fetching and processing of additional scripts, called importing.  Implementations that support modules need to ensure these scripts are processed the same as scripts processed directly.  Further, there may be additional privacy and security concerns depending on the location(s) the original script and its imported modules are obtained from.  For instance, a scripted obtained from "host-a.example" could request to import a script from "host-b.example", which could expose information about the executing environment (e.g., IP address) to "host-b.example".

With the addition of SharedArrayBuffer objects in ECMAScript version 8, it may be possible to implement a high-resolution timer which could lead to certain types of timing and side-channel attacks (e.g., {{SPECTRE}}).  Implementations may wish to take steps to mitigate this concern, such as disabling or removing support for SharedArrayBuffer objects, or take additional steps to ensure access to this shared memory is only accessible between execution contexts that have some form of mutual trust.

All other security considerations from {{RFC4329}} still apply.

# IANA Considerations

The media type registrations herein are divided into two major categories: the sole media type "text/javascript" which is now in common usage, and all of the media types that are obsolete.

For both categories, The ECMAScript media types are to be updated to point to a non-vendor specific standard undated specification of ECMAScript. In addition, a new file extension of .mjs is to be added to the list of file extensions with the restriction that it must correspond to the Module grammar of {{ECMA-262}}. Finally, the {{HTML}} specification uses "text/javascript" as the default media type of ECMAScript when preparing script tags; therefore, "text/javascript" intended usage is to be moved from OBSOLETE to COMMON.

## Common Javascript Media Types

### text/javascript

Type name:

: text

Subtype name:

: javascript

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: COMMON

Restrictions on usage:

: The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>


## Historic Javascript Media Types

The following media types are added or updated for historical purposes.  All herein have an intended usage of OBSOLETE, and are not expected to be in use with modern implementations.

### application/ecmascript

Type name:

: application

Subtype name:

: ecmascript

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .es, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.


Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>


### application/javascript

Type name:

: application

Subtype name:

: javascript

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.


Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org>.


### application/x-ecmascript

Type name:

: application

Subtype name:

: x-ecmascript

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .es, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.


Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>


### application/x-javascript

Type name:

: application

Subtype name:

: x-javascript

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.


Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>


### text/ecmascript

Type name:

: text

Subtype name:

: ecmascript

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .es, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.


Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>


### text/javascript1.0

Type name:

: text

Subtype name:

: javascript1.0

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.


Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>


### text/javascript1.1

Type name:

: text

Subtype name:

: javascript1.1

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>


### text/javascript1.2

Type name:

: text

Subtype name:

: javascript1.2

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>


### text/javascript1.3



Type name:

: text

Subtype name:

: javascript1.3

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>


### text/javascript1.4

Type name:

: text

Subtype name:

: javascript1.4

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>


### text/javascript1.5

Type name:

: text

Subtype name:

: javascript1.5

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>


### text/jscript

Type name:

: text

Subtype name:

: jscript

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>


### text/livescript

Type name:

: text

Subtype name:

: livescript

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>


### text/x-ecmascript

Type name:

: text

Subtype name:

: x-ecmascript

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .es, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>


### text/x-javascript

Type name:

: text

Subtype name:

: x-javascript

Required parameters:

: none

Optional parameters:

: charset, see section 4.1 of {{RFC4329}}.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}.

Published specification:

: \[\[RFCXXXX]]

Applications which use this media type:

: Script interpreters as discussed in {{RFC4329}}.

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section.

Intended usage:

: OBSOLETE

Restrictions on usage:

: The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>

--- back


# Acknowledgements

The authors would like to thank Suresh Krishnan, Alexey Melnikov, Mark Nottingham, James Snell, Adam Roach, and Allen Wirfs-Brock for their guidance throughout this process.
