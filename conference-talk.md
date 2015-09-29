---
title: Session Proposal Media Type
abbrev:
docname: draft-miller-session-proposal-01
date: 2015
category: info

ipr: ????
area: General
workgroup:
keyword: Internet-Draft

stand_alone: yes
pi: [toc, tocindent, sortrefs, symrefs, strict, compact, subcompact, comments, inline]

author:
 -
    ins: D. Miller
    name: Darrel Miller
    organization: Tavis Software Inc.
    email: darrel@tavis.ca
    uri: http://www.bizcoder.com


normative:
  RFC2119:
  RFC5234:
  RFC7230:
  RFC7231:
  RFC7234:

informative:
  RFC6265:



--- abstract

This draft document is a media type specification for describing a conference session proposal and the presenter(s).  This format aims to reduce the effort required for speakers to submit session proposals and for conference organizers to process those submissions.

--- note_Note_to_Readers

The issues list for this draft can be found at <https://github.com/darrelmiller/I-D/labels/session>.


--- middle

# Introduction
In the technology world, one way we share knowledge is via conferences.  In order to have a conference we need speakers to do talks.  Conferences commonly go through a process called "call for proposals" (CFP) where speakers who are interested submit talk proposals to the conference and then the conference organizers sift through these proposals and select the talks they believe will provide the best value to their attendees.

There are a very wide range of methods used by conferences for collecting these proposals:  Google docs, Excel spreadsheets, plain text emails, wikis, custom web sites, commercial conference management systems.  Each of these systems have slightly different ways of collecting information that is mostly the same.  

Many conferences are run by volunteers with minimal budgets and many speakers do so at their own expense.  Any possibility to improve the efficiency of the process of submitting proposals and processing them could provide significant value to a large number of conference participants.

# Goals
Easier for speakers to submit
 - Easy to author  (Need some kind of tooling)
 - No fancy formatting
 - Author once, submit anywhere
 - Hypermedia links to presenter info.

Easier for conference organizers to process
 - Simple for conference organizers to import
 - Zero UI submission process.
 - Easier to process submissions (queryable structures)
 - Standard UIs can be built to process submission format

# Usage Scenarios

There are a wide range of scenarios that could be enabled by this common format:
- Client Authoring tools that offer a good editing experience for creating new proposals.  
- Conference API for accepting proposals.
- Convert to HTML/PDF for submission to non-automated conferences or for publication of selected talks on conference website.
- Searchable respository of past talks with links to slides and videos.
- Central respository of available speakers talks.  Reverse the process so that conferences go looking for speakers instead of the other way around.

# Issues
 - Should talks be assigned a unique identifier, a version? A GUID?
 - Can exactly the same talk be done by a different person? Or is that a different talk?
 - Does an email address uniquely identify a speaker?  Should there be a different id?
 -Speaker availabilty could be a different document to allow conf organizers to find speakers.


## Examples

For example, a very minimal submission might look like this:

~~~
  { "proposal" : {
    "title" : "An Introduction To Media Type Design",
    "brief-description" : "Blah Blah Blah",
    "presenter" : {
      "name" : "Darrel Miller",
      "email" : "darrel@example.com"
      }
    }}
~~~
Note, that this representations is using JSON as a data format.

A more complete proposal might look like,
~~~
  [
  { "proposal" : {
    "title" : "An Introduction To Media Type Design",
    "brief-description" : "Blah Blah Blah",
    "full-description" : "Even longer blah Blah Blah",
    "keywords" : {
      "domain" : "http://stackoverflow.com/tags",
      "values":  ["javsascript", "java", "http"]
    },
    "length" : {
      "preferred" : 60,
      "min" : 45,
      "max" : 90
    }
    "presenter" : {
      "name" : "Darrel Miller",
      "email" : "darrel@example.com"
      }
    },
    "co-presenters" : [{
      "name" : "Bob Brown",
      "email" : "bob@example.com"
      }]
  }
  ]
~~~


## Notational Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT",
"RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in
{{RFC2119}}.

This document uses the Augmented Backus-Naur Form (ABNF) notation of {{RFC5234}} (including the
DQUOTE rule), and the list rule extension defined in {{RFC7230}}, Section 7. It includes by
reference the field-name, quoted-string and quoted-pair rules from that document, and the parameter
rule from {{RFC7231}}.


# Structure

This media type is design to hold information related to conference proposals, their presenters and the presentations of those sessions.

The root of the document should contain an array/list of structures, where each structure is identified by one of the following identifiers: proposal, presenter or presentation.

In JSON this might look like,
~~~
    [
     { "presenter" : {...} },
     { "proposal" : { ...} },
     { "proposal" : { ...} },
     { "presentation" : { ...} },
  ]
~~~
in XML, like this,
~~~
  <list>
     <presenter>...</presenter>
     <proposal>...</proposal>
     <proposal>...</proposal>
     <presentation>...</presentation>
  </list>
~~~
This specification does not define what the root XML element is called.

Allowing a list of structures allows the media type to support batch import operations and provide query results.  It also makes it easier to enable referencing document fragments for formats that support it.

## proposal
The proposal structure represents a description of a single conference session.  The only required property of the proposal structure is the title property.

### title
The title property is a single sentence description of the talk, normally used as a heading.  This is a required property.  Physical limits on the size of descriptive fields like this one are left to the choice of implementors.  If a specific implementation chooses to limit titles to 80 characters and it subsequently receives a document with a title that exceeds that amount, the implementation must choose whether to refuse the content, or to truncate it.

### brief-description
### full-description
### selection-notes
### keywords
### target-audience
### length
### languages

### co-presenters

## presenter
### name
### email

## presentation
### presentation-date
### conference
### video-recording
### slides



Descriptive content
  Title
  Brief description (For display on conference site)
  Long description
  Notes To Selection Committee
  Content Classification tags
  Audience Familiarity level
  Presentation History
    Conference
    Location
    Date
    Attendees
    Link To Video
  Length {Prefered, Max, Min}
  Languages []
  Style ( Keynote style  Workshop  lightning  Code heavy)
  link to slide deck
  Special Requirements

Presenter information
 Name
 Biography
 Speaking History
 Employer
 Contact information
   email
   Phone
 Airport
 Special Dietary Requirements
 T-shirt size
 Gender


Issues:
Field sizes...
How can tags be useful if not standardized "namespaced?"
content-classifications : [{
  "domain" : "http://stackoverflow.com"
  "tags": ["foo","bar"]
}]



Single or multiple sessions?



# Vocabulary



# IANA Considerations {#iana}


## Registrations




# Security Considerations


--- back

# Acknowledgements
