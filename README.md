# flymake-jshint

## Installation

To use JSHint with emacs, you will need JSHint installed and available on
your path. You should be able to do

   $ jshint

without problem. To do this, you can install node.js, npm and
jshint by doing the following:

    $ apt-get install nodejs # or your distro / OS equivalent
    $ sudo npm install -g jshint

You will probably want to configure the warnings that JSHint
produces. The full list is at http://www.jshint.com/options/ but
for reference I use:

```json
{ "browser": true, //browser constants, such as alert
  "curly": true, // require {} on one-line if
  "undef": true, // non-globals must be declared before use
  "newcap": true, // constructors must start with capital letter
  "jquery": true, // jQuery constants
  "nomen": false, // permit leading/trailing underscores, these do actually mean private in jQuery plugins
  "nonew": true, // don't permit object creation for side-effects only
  "strict": true // require "use strict";
}
```

Save this in a file called whatever.json and then set
`jshint-configuration-path` to point to it.

## Usage

Add to your emacs config:

```lisp
(require 'flymake-jshint)
(add-hook 'js-mode-hook 'flymake-mode)
```

making sure that flymake-jshint.el is on your load-path. If not,
also add to your config:

```lisp
(add-to-list 'load-path "~/.emacs.d/path/to/flymake-jshint.el")
```

## Debugging

If JSHint isn't working for any reason, execute

    M-x set-variable flymake-log-level <RET> 3

and you will see what is going wrong listed in the `*Messages*`
buffer.

## Alternatives

* https://github.com/lunaryorn/flycheck supports JSHint
* https://github.com/illusori/emacs-flymake is a fork of flymake
  that also supports JSHint (but does not support JSHint
  configuration)
* https://github.com/purcell/flymake-jslint will probably also
  work with JSHint

## Changelog

v2.1 -- We now create temporary files in the same directory as the
source file, so jshint can see .jshintrc configuration files.

v2.0 -- Updated usage instructions following the port to flymake-easy

v1.3 -- Refactored to use flymake-easy
