Goal
====

Practice using git like a pro, or as described here:
http://chris.beams.io/posts/git-commit/


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
