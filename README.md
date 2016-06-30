A PostScript unit test framework written in PostScript.


Example
=======

Code under test in file "readme-code.ps":

    /return-one 1 def
    /return-two 1 def

Test in file "readme-test.ps":

    (pstest.ps) runlibfile
    (readme-code.ps) run

    (Snippets for the Readme) test-case

    (return-one) should
    (return 1)
    return-one 1 assert-equal

    (return-two) should
    (return 2)
    return-two 2 assert-equal

    test-summary

Output in file "readme-expected.out":

    Snippets for the Readme
    .F
    --------------------------------------------------
    2 tests, 1 failed

    return-two
      should return 2
        expected: 2
        actual:   1


Definition
==========

Structure for code under test
-----------------------------

The code under test is a separate file that must run without side effects.
In particular, it should not make marks on the output device or modify
the stack in any way.

It should define a lot of procedures to exercise in the tests.

The procedures, when executed, could print debug messages.  They must
not leave anything on the stack that is not used up during the tests.

In addition you will want another PostScript program to later include
the no-side-effect module and actually do something useful with the
procedures defined.

Structure of a test case
------------------------

 * (pstest.ps) **runlibfile**
 * _filename-of-code-under-test_ **run**

Import the testing framework first, then the code under test.  Take
care not to redefine testing infrastructure accidentally.

 * _title_ **test-case** mark

A test is introduced by executing the procedure `test-case`. It reads
the title of the test case as a string and leaves a mark on the stack.

Assertions will leave all kinds of artifacts on the stack to describe
failed tests.

 * _item_ **should**

Group assertions as describing an item.

 * mark _any*_ **test-summary**

After the test, execute `test-summary`. This will print out all the
messages that have accumulated on the stack.

Test assertions
---------------

 * _spec actual_ **assert-true** _any*_

Pass if the value is true, fail otherwise.

 * _spec actual_ **assert-false** _any*_

Pass if the value is false, fail otherwise.

 * _spec actual expected_ **assert-equal** _any*_

Compares the two objects from the top of the stack.
If they are equal, the test is passed.

Otherwise prepares information so that the result is easier to
interpret.

 * _spec actual expected_ **assert-not-equal** _any*_

Compares the two objects from the top of the stack.
If they are _not_ equal, the test is passed.

Caveats
=======

This is more of a plaything than a serious endeavour.

There is no special construct to actually test some paint in the
output device.

When an error occurs, the program just breaks off with ghostscript's
standard error handling.  In particular, no further tests are
executed. [#18](https://github.com/tylus/pstest/issues/18)

There is no special construct to test error handling in an
application. [#15](https://github.com/tylus/pstest/issues/15)

The diff of objects is not very useful yet. For example, arrays are
always shown in full; contents of dicts are not shown at all.
[#16](https://github.com/tylus/pstest/issues/16)

The test summary is fragile: If any garbage is left on the stack by
the tests or code under test (especially marks), it will likely
produce garbage.


References
==========

Before you dig in here, know that [the Ghostscript project uses Python
unit tests](http://pages.cs.wisc.edu/~ghost/doc/AFPL/8.00/Testing.htm).

Otherwise my google-fu has deserted me.  I'm sure there must be dozens
of much more sophisticated PostScript unit test frameworks out there,
but I didn't find them.  While this is a fun project just to see
whether I can do it, if you know a better way, please let me know.

Ghostscript also has the only [coding
guidelines](http://www.ghostscript.com/doc/current/Ps-style.htm) of
which I am aware.  In this project, I have started to adopt that
style. Exceptions:

* I like `hyphenated-names` better than `camelCase` in PostScript.
* I don't put a copyright notice at the top of every file.
