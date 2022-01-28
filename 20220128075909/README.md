# Why I Avoid JavaScript if Possible

Recent security vulnerabilities like Log4shell (CVE-2021-44228) really
solidifies what a friend told me about not relying on a dependency unless
it's absolutely necessary.

Frontend web development is in my opinion, one of the most difficult of
all areas of IT. The reason is because frontend web development is all
about user experience (UX) and the user interface (UI). These two things
involve a mixture of graphic design, word smithing, and other skills I
don't have, nor care to learn. That being said, it is still important to
have enough knowledge to be proficient in creating a frontend web UI as a
backend developer.

The question then becomes "What do I learn for minimal frontend web
development?". AngularJS generates a massive amount of boilerplate code,
so that is not an option. I would never trust React due to the whole
licensing fiasco, which I recommend researching if you don't know about
it. Svelte is one I've heard a lot about but have yet to try. VueJS is
one I have had little experience with, but what I would choose to go with
if I had to use a JavaScript framework.

All the mentioned frameworks and all others have a bottleneck though in
my opinion, and that is `npm`, the primary JavaScript package manager.
Below I've included result of running `apt show npm` on Ubuntu 20.04.

As a challenge, see if you can think of a way to count the number of
packages listed by piping the output of `apt show npm`. I will give you a
hint with `apt show npm | grep "Depends:"`.

```BASH
Package: npm
Version: 6.14.4+ds-1ubuntu2
Priority: extra
Section: universe/web
Origin: Ubuntu
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Debian Javascript Maintainers <pkg-javascript-devel@lists.alioth.debian.org>
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Installed-Size: 3,468 kB
Depends: nodejs (>= 6.11~), ca-certificates, node-abbrev (>= 1.1.1~), node-ajv, node-ansi, node-ansi-regex (>= 3.0~), node-ansi-styles, node-ansistyles, node-aproba, node-archy (>= 1.0~), node-are-we-there-yet, node-asap, node-asn1, node-assert-plus, node-asynckit, node-aws4, node-aws-sign2, node-balanced-match, node-bcrypt-pbkdf, node-bl, node-bluebird, node-boxen, node-brace-expansion, node-builtin-modules, node-builtins, node-cacache, node-call-limit, node-camelcase, node-caseless, node-chalk, node-chownr, node-ci-info, node-cli-boxes, node-cliui, node-clone, node-co, node-color-convert, node-color-name, node-colors, node-columnify, node-combined-stream, node-concat-map, node-concat-stream, node-config-chain, node-configstore, node-console-control-strings, node-copy-concurrently, node-core-util-is, node-cross-spawn, node-crypto-random-string, node-cyclist, node-dashdash, node-debug, node-decamelize, node-deep-extend, node-defaults, node-define-properties, node-delayed-stream, node-delegates, node-detect-indent, node-detect-newline, node-dot-prop, node-duplexer3, node-duplexify, node-ecc-jsbn, node-editor, node-encoding, node-end-of-stream, node-err-code, node-errno, node-es6-promise, node-escape-string-regexp, node-execa, node-extend, node-extsprintf, node-fast-deep-equal, node-find-up, node-flush-write-stream, node-forever-agent, node-form-data, node-from2, node-fs.realpath, node-fs-vacuum, node-fs-write-stream-atomic, node-function-bind, node-gauge, node-genfun, node-get-caller-file, node-getpass, node-glob (>= 7.1.2~), node-got, node-graceful-fs (>= 4.1.11~), node-gyp (>= 3.6.2~), node-har-schema, node-har-validator, node-has-flag, node-has-unicode, node-hosted-git-info (>= 2.6~), node-http-signature, node-iconv-lite, node-iferr, node-import-lazy, node-imurmurhash, node-inflight, node-inherits (>= 2.0.3~), node-ini (>= 1.3.5~), node-invert-kv, node-ip, node-ip-regex, node-isarray, node-isexe, node-is-npm, node-is-obj, node-is-path-inside, node-is-retry-allowed, node-is-stream, node-isstream, node-is-typedarray, node-jsbn, node-jsonparse, node-json-parse-better-errors, node-json-schema, node-json-schema-traverse, node-jsonstream (>= 1.3.2~), node-json-stringify-safe, node-jsprim, node-latest-version, node-lazy-property, node-lcid, node-libnpx, node-locate-path, node-lodash, node-lockfile (>= 1.0.3~), node-lowercase-keys, node-lru-cache (>= 4.1.1~), node-make-dir, node-mem, node-mime, node-mime-types, node-mimic-fn, node-minimatch, node-minimist, node-mississippi, node-mkdirp (>= 0.5.1~), node-move-concurrently, node-ms, node-mute-stream, node-nopt, node-normalize-package-data (>= 2.4~), node-npm-bundled, node-npm-package-arg (>= 6.1.1), node-npmlog (>= 4.1.2~), node-number-is-nan, node-oauth-sign, node-object-assign, node-once (>= 1.4~), node-opener, node-osenv (>= 0.1.5~), node-os-locale, node-os-tmpdir, node-package-json, node-parallel-transform, node-path-exists, node-path-is-absolute, node-path-is-inside, node-promise-inflight, node-promise-retry, node-promzard, node-performance-now, node-p-finally, node-p-is-promise, node-pify, node-p-limit, node-p-locate, node-prepend-http, node-process-nextick-args, node-proto-list, node-prr, node-pseudomap, node-psl, node-pump, node-pumpify, node-punycode, node-qs, node-qw, node-rc, node-read (>= 1.0.7~), node-readable-stream, node-read-package-json (>= 2.0.13~), node-registry-auth-token, node-registry-url, node-request (>= 2.83~), node-require-main-filename, node-require-directory, node-resolve-from (>= 4.0~), node-retry (>= 0.10.1~), node-rimraf (>= 2.6.2~), node-run-queue, node-safe-buffer, node-semver (>= 5.5~), node-set-blocking, node-sha (>= 2.0.1~), node-shebang-command, node-shebang-regex, node-signal-exit, node-slide (>= 1.1.6~), node-sorted-object, node-slash, node-semver-diff, node-spdx-correct, node-spdx-exceptions, node-spdx-expression-parse, node-spdx-license-ids, node-sshpk, node-ssri, node-stream-each, node-stream-iterate, node-stream-shift, node-strict-uri-encode, node-string-decoder, node-string-width, node-strip-ansi (>= 4.0~), node-strip-json-comments, node-strip-eof, node-supports-color, node-tar (>= 4.4~), node-term-size, node-text-table, node-through, node-through2, node-timed-out, node-tough-cookie, node-tunnel-agent, node-tweetnacl, node-typedarray, node-uid-number, node-unique-filename, node-unique-string, node-unpipe, node-url-parse-lax, node-util-deprecate, node-uuid, node-validate-npm-package-name, node-verror, node-which (>= 1.3~), node-which-module, node-wide-align, node-widest-line, node-wrap-ansi, node-wrappy, node-wcwidth.js, node-write-file-atomic, node-xdg-basedir, node-xtend, node-yargs, node-yargs-parser, node-yallist, node-y18n
Homepage: https://docs.npmjs.com/
Download-Size: 583 kB
APT-Manual-Installed: yes
APT-Sources: http://us.archive.ubuntu.com/ubuntu focal/universe amd64 Packages
Description: package manager for Node.js
 Node.js is an event-based server-side javascript engine.
 .
 npm is the package manager for the Node JavaScript platform.  It puts
 modules in place so that node can find them, and manages dependency
 conflicts intelligently.
 .
 It is extremely configurable to support a wide variety of use cases.
 Most commonly, it is used to publish, discover, install, and develop
 node programs.
```

A popular alternative is `yarn` ...

```BASH
Package: yarnpkg
Version: 1.22.4-2
Priority: optional
Section: universe/javascript
Source: node-yarnpkg
Origin: Ubuntu
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Debian Javascript Maintainers <pkg-javascript-devel@lists.alioth.debian.org>
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Installed-Size: 3,159 kB
Provides: node-yarn
Depends: ca-certificates, node-asap, node-babel-runtime (>= 6.26.0), node-bytes (>= 3.0.0), node-camelcase (>= 4.0.0), node-chalk (>= 2.1.0), node-chownr, node-ci-info, node-cli-table, node-commander (>= 2.9.0), node-death, node-debug (>= 3.0.0), node-deep-equal, node-detect-indent, node-duplexify, node-emoji (>= 1.6.1), node-fast-levenshtein, node-glob (>= 7.1.1), node-imports-loader, node-ini (>= 1.3.4), node-inquirer (>= 3.3.0), node-invariant, node-is-builtin-module (>= 2.0.0), node-js-yaml (>= 3.13.1), node-loud-rejection, node-micromatch, node-minimatch (>= 2.3.11), node-mkdirp (>= 0.5.1), node-node-uuid (>= 3.0.1), node-object-path, node-path-root, node-proper-lockfile, node-puka, node-pump, node-pumpify, node-read (>= 1.0.7), node-request (>= 2.87.0), node-request-capture-har (>= 1.2.2), node-resolve, node-rimraf (>= 2.5.0), node-semver (>= 5.1.0), node-ssri, node-strict-uri-encode, node-strip-ansi (>= 4.0.0), node-strip-bom, node-tar-stream, node-validate-npm-package-license, node-yn, nodejs
Homepage: https://github.com/yarnpkg/yarn
Download-Size: 519 kB
APT-Sources: http://us.archive.ubuntu.com/ubuntu focal/universe amd64 Packages
Description: Fast, reliable and secure npm alternative
 Fast: Yarnpkg caches every package it has downloaded, so it never
 needs to download the same package again. It also does almost
 everything concurrently to maximize resource utilization.
 This means even faster installs.
 .
 Reliable: Using a detailed but concise lockfile format and a
 deterministic algorithm for install operations, Yarnpkg is able
 to guarantee that any installation that works on one system will
 work exactly the same on another system.
 .
 Secure: Yarnpkg uses checksums to verify the integrity of every
 installed package before its code is executed.
 .
 Node.js is an event-based server-side JavaScript engine.
```

`npm` alone is the reason why I choose to write HTML with Bootstrap 5 and
combine that with Go's `text/template` package to dynamically populate
content. The dilemma I am faced with is *when do I need to involve
VueJS?*. Time to look for an experienced frontend developer and pick
their brain.

Also for a bonus there is currently a common vulnerabilities and
exposures (CVE-2021-43616) open involving npm cli, where it will install
packages even if `package.json` doesn't match `package-lock.json`.

Related:

* Log4Shell
	<https://nvd.nist.gov/vuln/detail/CVE-2021-44228>
* Go `text/tempate`
	<https://pkg.go.dev/text/template>
* Fetch API 
	<https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API>
* VueJS
	<https://github.com/vuejs>
* svelte
	<https://github.com/sveltejs/svelte>
* `npm` JavaScript package manager
	<https://www.npmjs.com/>
* CVE-2021-43616
	<https://nvd.nist.gov/vuln/detail/CVE-2021-43616>
* npm cli issue for CVE-2021-43616
	<https://github.com/npm/cli/issues/2701>

Tags:

	#js #npm #vuejs #angularjs #react #go #cve-2021-43616
