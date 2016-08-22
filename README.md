# Itpl
# This file is released under the Python Software Foundation License v2,
# available at: http://www.opensource.org/licenses/PythonSoftFoundation.php

"""String interpolation for Python (by Ka-Ping Yee, 14 Feb 2000).

This module lets you quickly and conveniently interpolate values into
strings (in the flavour of Perl or Tcl, but with less extraneous
punctuation).  You get a bit more power than in the other languages,
because this module allows subscripting, slicing, function calls,
attribute lookup, or arbitrary expressions.  Variables and expressions
are evaluated in the namespace of the caller.

The itpl() function returns the result of interpolating a string, and
printpl() prints out an interpolated string.  Here are some examples:

    from Itpl import printpl
    printpl("Here is a $string.")
    printpl("Here is a $module.member.")
    printpl("Here is an $object.member.")
    printpl("Here is a $functioncall(with, arguments).")
    printpl("Here is an ${arbitrary + expression}.")
    printpl("Here is an $array[3] member.")
    printpl("Here is a $dictionary['member'].")

The filter() function filters a file object so that output through it
is interpolated.  This lets you produce the illusion that Python knows
how to do interpolation:

    import Itpl
    sys.stdout = Itpl.filter()
    f = "fancy"
    print "Isn't this $f?"
    print "Standard output has been replaced with a $sys.stdout object."
    sys.stdout = Itpl.unfilter()
    print "Okay, back $to $normal."

Under the hood, the Itpl class represents a string that knows how to
interpolate values.  An instance of the class parses the string once
upon initialization; the evaluation and substitution can then be done
each time the instance is evaluated with str(instance).  For example:

    from Itpl import Itpl
    s = Itpl("Here is $foo.")
    foo = 5
    print str(s)
    foo = "bar"
    print str(s)
"""
