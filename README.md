Goal
====

Practice using git like a pro, or as described
[by cbeams](http://chris.beams.io/posts/git-commit/).


Idea
====

Write a PostScript unit test framework.


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


Todo
====

* Start documentation of structure and assertions in readme
* Add disclaimer ('do not use')
* Publish on github
* Convert this todo list to issues on github?
* Add test for `util.ps`, i.e. `inc`
* Extend `test-this` to find tests by convention
* Pull out test failed / test passed
* Don't output current object twice if two tests fail for it
* Create shell script wrapper for convenience
* Add `assert-true`, `assert-false`
* Add verbose mode: show specs while they are tested
* Add `assert-not-equal`
* Add `assert-not-empty`
* Add `assert-contains`
* Add `assert-not-contains`
* Add `assert-deep-equal`
* Add `assert-almost-equal`
* Add `assert-deep-almost-equal`
