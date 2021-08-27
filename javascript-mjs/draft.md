---
title: ECMAScript Media Types Updates
abbrev:
docname: draft-ietf-dispatch-javascript-mjs-09
category: info

ipr: trust200902
area: ART
workgroup: DISPATCH
keyword: Internet-Draft
obsoletes: 4329

stand_alone: no
pi: [toc, tocindent, sortrefs, symrefs, strict, compact, comments, inline]

author:
 -
    ins: M. Miller
    name: Matthew A. Miller
    organization:
    email: linuxwolf+ietf@outer-planes.net
 -
    ins: M. Borins
    name: Myles Borins
    organization: GitHub
    email: mylesborins@github.com
 -
    ins: M. Bynens
    name: Mathias Bynens
    organization: Google
    email: mths@google.com
 -
    ins: B. Farias
    name: Bradley Farias
    organization:
    email: bradley.meck@gmail.com

normative:
  RFC2119:
  RFC2397:
  RFC2978:
  RFC3552:
  RFC3629:
  RFC4329:
  RFC6265:
  RFC8174:

  CHARSETS:
    author:
      org: IANA
    title: "Assigned character sets"
    target: https://www.iana.org/assignments/character-sets
  ECMA-262:
    author:
      org: Ecma International
    title: "Standard ECMA-262: ECMAScript Language Specification"
    date: June 2019
    target: https://ecma-international.org/publications/standards/Ecma-262.htm

informative:

  RFC3236:
  RFC3875:
  RFC3986:
  RFC3987:
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

This document describes the registration of media types for the ECMAScript and JavaScript programming languages and conformance requirements for implementations of these types. This document obsoletes RFC4329, "Scripting Media Types", replacing the previous registrations for "text/javascript" and "application/javascript" with information and requirements aligned with implementation experiences.

--- middle

# Introduction

This memo describes media types for the JavaScript and ECMAScript programming languages.  Refer to the sections "Introduction" and "Overview" in {{ECMA-262}} for background information on these languages.  This document updates the descriptions and registrations for these media types to reflect existing usage on the Internet.

This document replaces the media types registrations in {{RFC4329}}, obsoleting that document.

## Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14  {{RFC2119}}  {{RFC8174}} when, and only when, they appear in all capitals, as shown here.

# Compatibility

This document defines equivalent processing requirements for the types text/javascript, text/ecmascript, and application/javascript.  The most widely supported media type in use is text/javascript; all others are considered historical and obsolete compared to text/javascript.  Differences in ECMAScript versions have been better dealt with in the processors.

The types defined in this document are applicable to scripts written in {{ECMA-262}}.  This document does not address scripts written in other languages.  In particular, future editions of {{ECMA-262}} and extensions to {{ECMA-262}} are not directly addressed.

This document may be updated to take other content into account.  Updates of this document may introduce new optional parameters; implementations MUST consider the impact of such an update.

The definitions in this document reflect the current state of implementation across the JavaScript ecosystem, in web browsers and other environments such as Node.js alike, in order to guarantee backwards compatibility with existing applications as much as possible.

# Modules

In order to formalize support for modular programs, {{ECMA-262}} (starting with 6th Edition) defines two top-level goal symbols (or roots to the abstract syntax tree) for the ECMAScript grammar: Module and Script.  The Script goal represents the original structure where the code executes in the global scope, while the Module goal represents the module system built into ECMAScript starting with 6th Edition.  See the section "ECMAScript Language: Scripts and Modules" of {{ECMA-262}} for details.

This separation means that (in the absence of additional information) there are two possible interpretations for any given ECMAScript Source Text. The TC39 standards body for ECMAScript has determined that media types are outside of their scope of work {{TC39-MIME-ISSUE}}.

It is not possible to fully determine if a Source Text of ECMAScript is meant to be parsed in the Module or Script grammar goals based upon content alone. Therefore, scripting environments MUST use out of band information in order to determine what goal a Source Text should be treated as. To this end some scripting environments have chosen to adopt the new file extension of .mjs for this purpose.

This document does not define how fragment identifiers in resource identifiers ({{RFC3986}}, {{RFC3987}}) for documents labeled with one of the media types defined in this document are resolved.  An update of this document may define processing of fragment identifiers.

# Encoding

Refer to {{RFC6265}} for a discussion of terminology used in this section.  Source text (as defined in {{ECMA-262}}, section "Source Text") can be binary source text.  Binary source text is a textual data object that represents source text encoded using a character encoding scheme.  A textual data object is a whole text protocol message or a whole text document, or a part of it, that is treated separately for purposes of external storage and retrieval.  An implementation's internal representation of source text and source text are not considered binary source text.

Implementations need to determine a character encoding scheme in order to decode binary source text to source text.  The media types defined in this document allow an optional charset parameter to explicitly specify the character encoding scheme used to encode the source text.

How implementations determine the character encoding scheme can be subject to processing rules that are out of the scope of this document.  For example, transport protocols can require that a specific character encoding scheme is to be assumed if the optional charset parameter is not specified, or they can require that the charset parameter is used in certain cases.  Such requirements are not considered part of this document.

Implementations that support binary source text MUST support binary source text encoded using the UTF-8 {{RFC3629}} character encoding scheme.  Module goal sources MUST be encoded as UTF-8, all other encodings will fail.  Source goal sources SHOULD be encoded as UTF-8; other character encoding schemes MAY be supported, but are discouraged.

## Charset Parameter

The charset parameter provides a means to specify the character encoding scheme of binary source text.  Its value MUST match the mime-charset production defined in {{RFC2978}}, section 2.3, and SHOULD be a registered charset {{CHARSETS}}.  An illegal value is a value that does not match that production.

The charset parameter is only used when processing a Script goal source; Module goal sources MUST always be processed as UTF-8.

## Character Encoding Scheme Detection

It is possible that implementations cannot interoperably determine a single character encoding scheme simply by complying with all requirements of the applicable specifications.  To foster interoperability in such cases, the following algorithm is defined.  Implementations apply this algorithm until a single character encoding scheme is determined.

1. If the binary source text is not already determined to be a Module goal and starts with a Unicode encoding form signature, the signature determines the encoding.  The following octet sequences, at the very beginning of the binary source text, are considered with their corresponding character encoding schemes:

        +------------------+----------+
        | Leading sequence | Encoding |
        |------------------+----------|
        | EF BB BF         | UTF-8    |
        | FF FE            | UTF-16LE |
        | FE FF            | UTF-16BE |
        +------------------+----------+

    Implementations of this step MUST use these octet sequences to determine the character encoding scheme, even if the determined scheme is not supported.  If this step determines the character encoding scheme, the octet sequence representing the Unicode encoding form signature MUST be ignored when decoding the binary source text.

2. If a charset parameter with a legal and understood value is specified, the value determines the character encoding scheme.

3. If no other character encoding scheme is determined from the previous steps, it is assumed to be UTF-8.

If the character encoding scheme is determined to be UTF-8 through any means other than step 1 as defined above and the binary source text starts with the octet sequence EF BB BF, the octet sequence is ignored when decoding the binary source text.

## Character Encoding Scheme Error Handling

Binary source text that is not properly encoded for the determined character encoding can pose a security risk, as discussed in section 5.  That said, because of the varied and complex environments scripts are executed in, most of the error handling specifics are left to the processors.  The following are broad guidelines that processors follow.

If binary source text is determined to have been encoded using a certain character encoding scheme that the implementation is unable to process, implementations can consider the resource unsupported (i.e., do not decode the binary source text using a different character encoding scheme).

Binary source text can be determined to have been encoded using a certain character encoding scheme but contain octet sequences that are not legal according to that scheme.  Implementations can substitute those illegal sequences with the replacement character U+FFFD (properly encoded for the scheme), or stop processing altogether.

# Security Considerations

Refer to {{RFC3552}} for a discussion of terminology used in this section.  Examples in this section and discussions of interactions of host environments with scripts, modules, and extensions to {{ECMA-262}} are to be understood as non-exhaustive and of a purely illustrative nature.

The programming language defined in {{ECMA-262}} is not intended to be computationally self-sufficient, rather it is expected that the computational environment provides facilities to programs to enable specific functionality.  Such facilities constitute unknown factors and are thus considered out of the scope of this document.

Derived programming languages are permitted to include additional functionality that is not described in {{ECMA-262}}; such functionality constitutes an unknown factor and is thus considered out of the scope of this document.  In particular, extensions to {{ECMA-262}} defined for the JavaScript programming language are not discussed in this document.

Uncontrolled execution of scripts can be exceedingly dangerous. Implementations that execute scripts MUST give consideration to their application's threat models and those of the individual features they implement; in particular, they MUST ensure that untrusted content is not executed in an unprotected environment.

Module scripts in ECMAScript can request the fetching and processing of additional scripts, called importing.  Implementations that support modules need to process imported sources in the same way scripts.  Further, there may be additional privacy and security concerns depending on the location(s) the original script and its imported modules are obtained from.  For instance, a script obtained from "host-a.example" could request to import a script from "host-b.example", which could expose information about the executing environment (e.g., IP address) to "host-b.example".  See the section "ECMAScript Language: Scripts and Modules" in {{ECMA-262}} for details.

Specifications for host environment facilities and for derived programming languages should include security considerations.  If an implementation supports such facilities, the respective security considerations apply.  In particular, if scripts can be referenced from or included in specific document formats, the considerations for the embedding or referencing document format apply.

For example, scripts embedded in application/xhtml+xml {{RFC3236}} documents could be enabled through the host environment to manipulate the document instance, which could cause the retrieval of remote resources; security considerations regarding retrieval of remote resources of the embedding document would apply in this case.

This circumstance can further be used to make information, that is normally only available to the script, available to a web server by encoding the information in the resource identifier of the resource, which can further enable eavesdropping attacks.  Implementation of such facilities is subject to the security considerations of the host environment, as discussed above.

The programming language defined in {{ECMA-262}} does include facilities to loop, cause computationally complex operations, or consume large amounts of memory; this includes, but is not limited to, facilities that allow dynamically generated source text to be executed (e.g., the eval() function); uncontrolled execution of such features can cause denial of service, which implementations MUST protect against.

With the addition of SharedArrayBuffer objects in ECMAScript version 8, it could be possible to implement a high-resolution timer which could lead to certain types of timin`g and side-channel attacks (e.g., {{SPECTRE}}).  Implementations can take steps to mitigate this concern, such as disabling or removing support for SharedArrayBuffer objects, or take additional steps to ensure access to this shared memory is only accessible between execution contexts that have some form of mutual trust.

A host environment can provide facilities to access external input. Scripts that pass such input to the eval() function or similar language features can be vulnerable to code injection attacks. Scripts are expected to protect against such attacks.

A host environment can provide facilities to output computed results in a user-visible manner.  For example, host environments supporting a graphical user interface can provide facilities that enable scripts to present certain messages to the user.  Implementations MUST take steps to avoid confusion of the origin of such messages.  In general, the security considerations for the host environment apply in such a case as discussed above.

Implementations are required to support the UTF-8 character encoding scheme; the security considerations of {{RFC3629}} apply.  Additional character encoding schemes may be supported; support for such schemes is subject to the security considerations of those schemes.

Source text is expected to be in Unicode Normalization Form C. Scripts and implementations MUST consider security implications of unnormalized source text and data.  For a detailed discussion of such implications refer to the security considerations in {{RFC3629}}.

Scripts can be executed in an environment that is vulnerable to code injection attacks.  For example, a CGI script {{RFC3875}} echoing user input could allow the inclusion of untrusted scripts that could be executed in an otherwise trusted environment.  This threat scenario is subject to security considerations that are out of the scope of this document.

The "data" resource identifier scheme {{RFC2397}}, in combination with the types defined in this document, could be used to cause execution of untrusted scripts through the inclusion of untrusted resource identifiers in otherwise trusted content.  Security considerations of {{RFC2397}} apply.

Implementations can fail to implement a specific security model or other means to prevent possibly dangerous operations.  Such failure could possibly be exploited to gain unauthorized access to a system or sensitive information; such failure constitutes an unknown factor and is thus considered out of the scope of this document.

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

: N/A

Optional parameters:

: charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: COMMON

Restrictions on usage:

: The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section of \[this document].

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

: N/A

Optional parameters:

: charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .es, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.


Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org\>


### application/javascript

Type name:

: application

Subtype name:

: javascript

Required parameters:

: N/A

Optional parameters:

: charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: charset, see section 4.1 of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.


Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org>.


### application/x-ecmascript

Type name:

: application

Subtype name:

: x-ecmascript

Required parameters:

: N/A

Optional parameters:

: : charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .es, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.


Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org\>


### application/x-javascript

Type name:

: application

Subtype name:

: x-javascript

Required parameters:

: N/A

Optional parameters:

: : charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.


Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org\>


### text/ecmascript

Type name:

: text

Subtype name:

: ecmascript

Required parameters:

: N/A

Optional parameters:

: : charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .es, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.


Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org\>


### text/javascript1.0

Type name:

: text

Subtype name:

: javascript1.0

Required parameters:

: N/A

Optional parameters:

: : charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.


Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org\>


### text/javascript1.1

Type name:

: text

Subtype name:

: javascript1.1

Required parameters:

: N/A

Optional parameters:

: : charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org\>


### text/javascript1.2

Type name:

: text

Subtype name:

: javascript1.2

Required parameters:

: N/A

Optional parameters:

: : charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org\>


### text/javascript1.3



Type name:

: text

Subtype name:

: javascript1.3

Required parameters:

: N/A

Optional parameters:

: : charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org\>


### text/javascript1.4

Type name:

: text

Subtype name:

: javascript1.4

Required parameters:

: N/A

Optional parameters:

: : charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org\>


### text/javascript1.5

Type name:

: text

Subtype name:

: javascript1.5

Required parameters:

: N/A

Optional parameters:

: : charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: This media type is obsolete; current implementations should use text/javascript as the only JavaScript/ECMAScript media type. The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org\>


### text/jscript

Type name:

: text

Subtype name:

: jscript

Required parameters:

: N/A

Optional parameters:

: : charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org\>


### text/livescript

Type name:

: text

Subtype name:

: livescript

Required parameters:

: N/A

Optional parameters:

: : charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org\>


### text/x-ecmascript

Type name:

: text

Subtype name:

: x-ecmascript

Required parameters:

: N/A

Optional parameters:

: : charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .es, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org\>


### text/x-javascript

Type name:

: text

Subtype name:

: x-javascript

Required parameters:

: N/A

Optional parameters:

: : charset, see section 4.1 of \[this document].

Encoding considerations:

: Binary

Security considerations:

: See section 5 of \[this document]..

Interoperability considerations:

: See various sections of \[this document].

Published specification:

: \[this document]

Applications which use this media type:

: Script interpreters as discussed in \[this document].

Additional information:

: Magic number(s):

  : n/a

  File extension(s):

  : .js, .mjs

  Macintosh File Type Code(s):

  : TEXT

Person & email address to contact for further information:

: See Author's Address section of \[this document].

Intended usage:

: OBSOLETE

Restrictions on usage:

: The .mjs file extension signals that the file represents a JavaScript module. Execution environments that rely on file extensions to determine how to process inputs parse .mjs files using the Module grammar of {{ECMA-262}}.

Author:

: See Author's Address section of \[this document].

Change controller:

: IESG \<iesg@ietf.org\>

--- back


# Acknowledgements

This work builds upon its antecedent document, authored by Bjoern Hoehrmann.  The authors would like to thank Adam Roach, Anne van Kesteren, Allen Wirfs-Brock, Alexey Melnikov, James Snell, Mark Nottingham, Murray Kucherawy, and Suresh Krishnan for their guidance and feedback throughout this process.

# Changes from RFC 4329

* Added a section discussing ECMAscript modules and the impact on processing.
* Updated the Security Considerations to discuss concerns associated with ECMAscript modules and SharedArrayBuffers.
* Updated the character encoding scheme detection to remove normative guidance on its use, to better reflect operational reality.
* Changed the intended usage of the media type text/javascript from obsolete to common.
* Changed the intended usage for all other script media types to obsolete.
* Updated various references where the original has been osboleted
* Updated references to ECMA-262 to match the version at time of publication.
