Regular Expressions
===================

.. index::
   single: Regular Expressions
   single: Regex

So far we have been reading through files, looking for patterns and
extracting various bits of lines that we find interesting. We have been using string methods like ``split`` and ``find`` and using lists and string slicing to extract portions of the lines.


This task of searching and extracting is so common that Python has a
very powerful library called *regular expressions* that
handles many of these tasks quite elegantly. The reason we have not
introduced regular expressions earlier in the book is because while they
are very powerful, they are a little complicated and their syntax takes
some getting used to.

Regular expressions are almost their own little programming language for
searching and parsing strings. As a matter of fact, entire books have
been written on the topic of regular expressions. In this chapter, we
will only cover the basics of regular expressions. For more detail on
regular expressions, see:

https://en.wikipedia.org/wiki/Regular_expression

https://docs.python.org/library/re.html

The regular expression library ``re`` must be imported into
your program before you can use it. The simplest use of the regular
expression library is the ``search()`` function. The following
program demonstrates a trivial use of the search function.

.. code-block:: python

   # Search for lines that contain 'From:'
   import re
   hand = open('mbox-short.txt')
   for line in hand:
       line = line.rstrip()
       if re.search('From:', line):
           print(line)

We open the file, loop through each line, and use the regular expression
``search()`` to only print out lines that contain the string
"From:". This program does not use the real power of regular
expressions, since we could have just as easily used
``line.find()`` to accomplish the same result.

.. mchoice:: question11_1_1
   :practice: T
   :answer_a: import regex
   :answer_b: import re.search()
   :answer_c: import re
   :correct: c
   :feedback_a: Try again!
   :feedback_b: Try again!
   :feedback_c: Correct! This is the proper way to import the regular expression library.

   Which method correctly imports the regex library?

The power of the regular expressions comes when we add special
characters to the search string that allow us to more precisely control
which lines match the string. Adding these special characters to our
regular expression allow us to do sophisticated matching and extraction
while writing very little code.

For example, the caret character is used in regular expressions to match
"the beginning" of a line. We could change our program to only match
lines where "From:" was at the beginning of the line as follows:

.. code-block:: python

   # Search for lines that start with 'From:'
   import re
   hand = open('mbox-short.txt')
   for line in hand:
       line = line.rstrip()
       if re.search('^From:', line):
           print(line)

Now we will only match lines that *start with* the string
"From:". This is still a very simple example that we could have done
equivalently with the ``startswith()`` method from the string
library. But it serves to introduce the notion that regular expressions
contain special action characters that give us more control as to what
will match the regular expression.

.. mchoice:: question11_1_2
   :practice: T
   :answer_a: Any line that contains a 'B'
   :answer_b: Any line containing 'b'
   :answer_c: Lines starting with the letter 'b'
   :correct: b
   :feedback_a: Try again!
   :feedback_b: Correct! Since there is no ^ before the 'b', we are only looking at lines that contain the letter 'b'.
   :feedback_c: Try again!

   Which lines will the following code print?

   .. code-block:: python

      import re
      hand = open('mbox-short.txt')
      for line in hand:
          line = line.rstrip()
          if re.search('b', line):
              print(line)


.. parsonsprob:: question11_1_3
   :numbered: left
   :practice: T
   :adaptive:

   Construct a block of code that sorts through a file and prints out any line starting with 'Wolverines'.
   -----
   import re
   =====
   hand = open('mbox-short.txt')
   =====
   for line in hand:
   =====
    line = line.split() #distractor
   =====
    line = line.rstrip()
   =====
    if re.search('Wolverines', line): #distractor
   =====
    if re.search('^Wolverines', line):
   =====
     print(line)
