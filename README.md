# manifest-v3-csp-bug-ex

An example of CSP not being used with a Manifest V3 web extension

## About

What steps will reproduce the problem?
(1) Clone example repo: https://github.com/samrum/manifest-v3-csp-bug-ex
(2) Build extension and start Vite dev server: npm install; npm run dev
(3) Load dist directory in chrome browser either manually or using: npm run serve:chrome
(4) Open options page of extension

What is the expected result?
http://localhost:3000/src/options/main.js is loaded by options page html and renders page content

What happens instead?
CSP defined in manifest.json isn't followed or used, http://localhost:3000/src/options/main.js is blocked:

Refused to load the script 'http://localhost:3000/src/options/main.js' because it violates the following Content Security Policy directive: "script-src 'self'". Note that 'script-src-elem' was not explicitly set, so 'script-src' is used as a fallback.

Please provide any additional information below. Attach a screenshot if
possible.

Also applies to action.default_popup html file as well as injected content script

manifest.json of extension is using this CSP definition:

	"content_security_policy": {
		"extension_pages": "script-src http://localhost:3000; object-src 'self'"
	}

In manifest V2, the equivalent CSP works:

	"content_security_policy": "script-src http://localhost:3000; object-src 'self'"

