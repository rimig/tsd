# TSD 0.5.x TODO

> Big list of things that should/could be done.

See also:

* Main [readme](../README.md)
* Project [scope](SCOPE.md)
* Some extra [info](INFO.md)
* More about [code](CODE.md)

## Issues

This info might later migrate to the Github Issue tracker.

## Update docs

Always text to edit in the README or ./docs.

## Local changes

Browse the code in `/src` and `/test` for `//TODO` comments,

Or use `$ grunt todos` for an overview. :point_left::+1:

Most of these are file/class/block 'local' changes: easy to fix without conflicts (hardening, re-implement etc). Some are more important then others (but which ones? :smiley_cat:)

## Tests

Never enough.

* :a:   Expand API command testing; besides search/install ~~(once update fixtures land)~~
* :x:   Add CLI tests
* :o:	Add node.js module tests
* :id:	Consider testing JavaScript output instead of TypeScript source.

Working on a way run data tests from fixtures that can be updated easily (otherwise decent coverage is insane to manage) 

* :m:	Run github api+raw caches from fixtures (with easy updates/expansion)
* :m:   Run API tests from fixtures and stored comparison output (with easy updates/expansion)

## Global / multi-file changes:

### Commands

Basics commands

* :m:	Add help (show commands) 
* :m:	Add version (show version)
* :x:	Add init (new json with repo/branch)
* :m:	Add settings (show config info)
* :m:	Add reinstall (from config)
* :vs:	Consider unifying local/remote selectors (tricky)

Remote selector commands

* :m:	Add search (search definitions)
* :m:	Add install (install definitions)
* :o:	Add direct (install from commit sha, or blob)
* :m:	Add info (parse file content)
* :m:	Add history (list commit history)
* :o:	Add details (detailed commit history), needed?
* :x:	Enhance deps (list dependencies), make recursive and display

Local selector commands

* :x:	Add local (search local files)
* :x:	Add uninstall (remove local files)
* :x:	Add compare (check for updates)
* :x:	Add update (apply updates)

Browser commands

* :o:	Add feature to open a browser to see the pages on github? (diffs, comments etc) :zap:
* :o:	Add feature to open a browser at a project's url (from info) :zap:

UIX commands

* :o:	Add auto/scan command (suggest appropriate definitions from package.json/bower.json) (@seanhess: see [codeplex](https://typescript.codeplex.com/discussions/461449) and [TPM](https://github.com/seanhess/TPM))
* :id:	Consider adding reference/bundle command to generate typing collections (save in config)

Cache commands

* :b:	Add purge (or flush)
* :b:	Add dump (see content)

Selector

* :x:	Improve globbing/RegExp :zap:
* :x:	Add support for semver :zap:
* :x:	Add support for multiple Selectors (blend results in select()) :zap:
* :x:	Add InfoMatcher to Selector / select() :zap:
* :o:	Add search-by-date to history-command, add as DateMatcher to Selector / select()

Command options

* :a:   Plan options and unify the names (both for CLI as API)
* :b:	Add option for file overwrite (always on now)
* :x:	Add a compact vs detailed option (for search listings or history)
* :ab:	Add option for dependency install (always on now)
* :x:	Add option for selection-match-count limiter; so user don't accidentally bust their rate limit using `$ tsd history  *` etc
* :o:	.... more

Functionality

* :o2:	Handle rate-limit properly
* :id:	Add github credentials (or tsdpm-proxy) to bypass busted rate limits (for bulk commands)
* :id:	Add fancy promise progress events + cli display (install etc)

CLI

* :m:	Improve Expose for crisper CLI help screen layout (table/columns)
* :m:   Improve Expose to order/group commands :zap:
* :x:	Optimise and unify CLI output (indenting/seperator/headers etc) :zap:
* :o:	Improve CLI with [w-m/pleonasm](http://w-m.github.io/pleonasm/) :zap:
* :x:	Add TSD release/updates news to CLI console (periodically pull json from github) :zap:

API

* :o:	Export API docs during build :zap:
* :o:	Export TypeScript definitions :zap:
* :id:	Consider optimising or wrapping the JavaScript API (less OO-ish)
* :id:	Add options to authenticate to github API for higher rate-limit

Data model/repo

* :o:	Harden JSON import
* :id:	Consider decoupling from Github json format (abstract service)
* :id:	Consider adapting to work from a git-checkout (abstract service)

Info

* :m:	Import tests for header parser from tsd-deftools @bartvds
* :o:	Improve DefInfo/Parser to extract more info from more files :zap:

Config

* :m:	Improve config JSON-Schema (RegExp)
* :o:	Improve config validation reporting (see tv4, chai-json-schema)
* :m:	Consider renaming 'tsd-config.json' to 'tsd.json'

Cache

* :m:	Decide on user caching directory: home / AppData like npm
* :m:	Decide on cache folder version naming scheme
* :b:	Add cache auto-refresh; for the non-unique queries like `getBranch`
* :a:	Drop 'node-github' dependency and self re-implement github API to leverage http-cache-headers (and rate limit timeout info)
* :b:	Add periodic automated cache purge/flush
* :m:	Add skip features to loaders; enforce for testing from local fixtures. 
* :o:	Consider blob cache by resolving commit sha to blob in a history; cache mappings; calc sha from content
* :vs:	Consider g-zip for caches

Internals

* :a:	Try recalculating sha1 hash from content (fix: weird error in #master `$ tsd install chai` (fixed by forced line-ends?)
* :b:	Add local-changes detector using the hash / sha
* :m:	Change Context objects to use Q/Q-io and not auto-create folders at init
* :vs:	Decide if API, Core etc need(more) race condition hardening
* :vs:	Consider if API and/or Core need to be split into command classes.
* :vs:	Consider adding timeouts
* :id:	Consider splitting Core.ts: index/select stuff vs helper methods/objects
* :o:	Consider global store for JSON pointers and RegExps etc
* :cl:	Clean up usage of module name within same module (eg: `tsd.Def` is not needed in other code inside the `tsd` module (could be a remnant of old TS 0.8 or a old WebStorm 6 glitch fix).
* :o:	Add xm interface for debug/log/event tracking
* :cl:	Unify `xm.StatCounter` & `xm.Logger` into event tracker (and link child objects) (started in EventLog.ts)

Technical

* :a:	Move to TS 0.9 generics definition of Q promises (in progress)
* :o2:	Expand property / const immutability: Object.freeze()
* :o2:	Ditch more getters + private vars for Object.freeze() (`xm.ObjectUtils`)
* :cl:	Change some utils from static class members to module functions

Cleanup

* :cl:	Sweep and enable `tslint.json` rules
* :cl:	Clean `package.json`: fix some ~tildes before release
* :cl:	Sweep used modules: require() and `package.json`, dev vs runtime, npm prune 
* :cl:	Sweep facing code (API / Context etc) for input parameter checking(`xm.assertVar`) :zap:
* :cl:	Sweep and optimise reference-paths (but how? find auto-tool?) :zap:
* :m:	Verify "use strict" (needed in node?)

Publishing

* :o2:	Add npm pre-publish tests hook :zap:
* :x:	Add git pre-commit test hook :zap:
* :vs:	Decide docs use of name-casing: use either TSD or tsd? (npm and bower are lowercase)
* :vs:	Decide & sweep title/description text (package.json, cli/api, github etc) :zap:
* :vs:	Decide solution to update TSDPM.com: module and authenticated github with a DefinitelyTyped hook to heroku.
* :m:	Fix bin/cli `$ npm install . -g` 
* :m:	Fix bin/cli `$ npm install git://github.com/Diullei/tsd#develop-0.5.x -g`
* :x:	Compile a build number + date into application :zap:
* :x:	Credits :smiley_cat:

Dependencies

* :id:	Consider dropping underscore?
* :a:	Update Q with generics
* :o:	Sweep recent xm `package changes for new tests 

Bugs:

* :o:	Installing `$ tsd install chai` gives content error
* :o:	Installing `$ tsd search q` / `$ tsd search q/*` doesn't work properly
* :o:	Underscore.d.ts header has multiple authors

More.. always more :rocket:

## Emoji based Project Management 

Status indicators:

* :m:	Resolved and closed (*'mint!'*).
* :id:	Proposal or idea for consideration.
* :vs:	Decision needed (this vs that).
* :sa:	Pending (reaction / remote fix).
* :a:	First priority.
* :b:	Second priority.
* :ab:	Important non-prioritised.
* :cl:	Need to clean up.
* :o2:	Must resolve for release.
* :x:	Acknowledged, waiting for priority.
* :o:	Open, incoming, undetermined.

Reserved (short codes):

* :ok:	Decision made?
* :ng:	(angular :)
* :up:	Released?
* :cd:	Shipped? Released?
* :on:
* :tm:
* :+1:
* :-1:
* :v:
