---
title: ECMAScript Media Types Updates
abbrev:
docname: draft-ietf-dispatch-javascript-mjs-03
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
    target: http://www.ecma-international.org/publications/standards/Ecma-262.htm

informative:

  HTML:
    author:
      org: WHATWG
    title: HTML Living Standard
    date: August 2017
    target: https://html.spec.whatwg.org/multipage/scripting.html#prepare-a-script

  TC39-MIME-ISSUE:
    author:
      org: TC39
    title: "Add `application/javascript+module` mime to remove ambiguity5"
    date: August 2017
    target: https://web.archive.org/web/20170814193912/https://github.com/tc39/ecma262/issues/322


--- abstract

This document proposes updates to the ECMAScript media types, superseding the existing registrations for "application/javascript" and "text/javascript" by adding an additional extension and removing usage warnings.  This document updates RFC4329, "Scripting Media Types".

--- note_Note_to_Readers

The issues list for this draft can be found at <https://github.com/bmeck/I-D/labels/javascript-mjs>.

The most recent (often, unpublished) draft is at <https://github.com/bmeck/I-D/tree/master/javascript-mjs>.

Recent changes are listed at <https://github.com/bmeck/I-D/commits/master/javascript-mjs>.

--- middle


# Introduction

This document updates the existing media types for the ECMAScript programming language. It supersedes the media types registrations in {{RFC4329}} for "application/javascript" and "text/javascript".


# Background

In order to formalize support for modular programs {{ECMA-262}} now defines two top-level goal symbols for the ECMAScript grammar. This means that (in the absence of additional information) there are two possible interpretations for any given ECMAScript Source Text. The TC39 standards body for ECMAScript has determined that media types are outside of their scope of work {{TC39-MIME-ISSUE}}.

It is not possible to fully determine if a Source Text of ECMAScript is meant to be parsed in the Module or Script grammar goals based upon content alone. Therefore, scripting environments must use out of band information in order to determine what goal a Source Text should be treated as. To this end some scripting environments have chosen to adopt a new file extension of .mjs for determining the goal of a given Source Text.


# IANA Considerations

The media type registrations herein are divided into two major categories: the sole media type "text/javascript" which is now in common usage, and all of the media types that are obsolete.

For both categories, The ECMAScript media types are to be updated to point to a non-vendor specific standard undated specification of ECMAScript. In addition, a new file extension of .mjs is to be added to the list of file extensions with the restriction that it must correspond to the Module grammar of {{ECMA-262}}. Finally, the {{HTML}} specification is using "text/javascript" as the default media type of ECMAScript when preparing script tags; therefore, "text/javascript" has been moved intended usage from OBSOLETE to COMMON.

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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}

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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: This media type is obsolete; current implementations should use text/javascript as the only javascript/ECMAscript media type. The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}

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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: This media type is obsolete; current implementations should use text/javascript as the only javascript/ECMAscript media type. The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}


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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: This media type is obsolete; current implementations should use text/javascript as the only javascript/ECMAscript media type. The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}


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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: This media type is obsolete; current implementations should use text/javascript as the only javascript/ECMAscript media type. The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}


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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: This media type is obsolete; current implementations should use text/javascript as the only javascript/ECMAscript media type. The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}


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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: This media type is obsolete; current implementations should use text/javascript as the only javascript/ECMAscript media type. The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}


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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: This media type is obsolete; current implementations should use text/javascript as the only javascript/ECMAscript media type. The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}

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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: This media type is obsolete; current implementations should use text/javascript as the only javascript/ECMAscript media type. The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}

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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: This media type is obsolete; current implementations should use text/javascript as the only javascript/ECMAscript media type. The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}

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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: This media type is obsolete; current implementations should use text/javascript as the only javascript/ECMAscript media type. The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}

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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: This media type is obsolete; current implementations should use text/javascript as the only javascript/ECMAscript media type. The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}

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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}

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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}

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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}

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
: goal, declares the goal symbol in the Syntactic Grammars of {{ECMA-262}} to be used while parsing. This parameter is case insensitive.

Encoding considerations:

: Encoding is host dependent with differences in byte order marks, the charset parameter, and text preprocessing.

Security considerations:

: See section 5 of {{RFC4329}}.

Interoperability considerations:

: See notes in various sections of {{RFC4329}}. This media type does not specify the grammar of {{ECMA-262}} used when missing the goal parameter.

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

: The file extension .mjs must be parsed using the Module grammar of {{ECMA-262}}

Author:

: See Author's Address section.

Change controller:

: IESG \<iesg@ietf.org\>

--- back


# Acknowledgements

Thanks to Suresh Krishnan, Alexey Melnikov, Mark Nottingham, James Snell, Adam Roach, and Allen Wirfs-Brock for guiding me through this process.
