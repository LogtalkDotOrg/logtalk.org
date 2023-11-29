---
layout: article
permalink: backend_requirements.html
title: Backend Prolog compiler requirements
aside:
  toc: true
---

Logtalk requires a backend Prolog compiler that supports **both** official and de facto Prolog standards. This means, support for the ISO Prolog Core standard plus the following de facto standard predicates:

* `predicate_property/2`
* `setup_call_cleanup/3`
* `between/3`
* `numbervars/3`
* `format/2-3`

The `setup_call_cleanup/3` predicate is only required for systems providing a compatible threads implementation and for support of some tools features that require checking query determinism. In the second case, it can be replaced by `call_cleanup/2` or `call_det/2` predicates.

Logtalk coinduction features requires that the backend Prolog compiler supports cyclic terms and either the `*->/2` soft-cut control construct or the `if/3` soft-cut built-in predicate.

The de facto standard `dialect` and `version_data` flags are required. Notably, the `version_data` flag is used at Logtalk startup to check that its running on a supported Prolog backend versions and used by tools such as `lgtunit` to add version information to testing log files.

In addition, Logtalk requires basic access to the operating-system (either as Prolog built-in predicates or as library predicates) including:

* expanding a relative path into an absolute path (including paths with environment variables)
* converting between Prolog internal paths and operating-systems paths (if necessary)
* file and directory existence testing
* file size and modification time
* file copying, renaming, and deleting
* file permissions (read, write, execute)
* querying and changing the current working directory
* directory creating and deleting
* current date and time
* access to cpu and wall time
* accessing environment variable values
* querying the process identifier
* computing an atom hash

These operating-system access predicates are used in the Prolog compiler adapter file and in the portable operating-system library.

Convenient features include the de facto standard `findall/4` predicate and access via `read_term/3` or `stream_property/2` to a read term position (line numbers).
