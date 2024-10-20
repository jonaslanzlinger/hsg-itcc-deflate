# LZ77 - Overlap Example

<em>Insprired by [Antaeus Feldspar](https://www.cs.ucdavis.edu/~martel/122a/deflate.html)</em>

***

This is an example of highly compressible data through overlap between match and current coding position.

Consider the following input string:
    
    Blah blah blah blah blah!

This highly compressible data can be compressed to just this:
    
    Blah b[D=5, L=18]!

Why this? The input stream starts by receiving the characters:

    "B", "l", "a", "h", " ", "b".

Those characters are simply directed to the output data. But now, look at the next character "l". Here, you may recognize, that we have a match with the first "l" in the sliding window.
Therefore, we check, how long this match is:
* "l" is matching
* "a" is also matching
* "h" is also matching
* " " is also matching
* "b" is also matching
* Now, we match over the current coding position...
* "l" is matching again
* "a" is matching again
* ...and so on...

Let us now also decompress the compressed data into the original string:

    Blah b[D=5, L=18]!

We simply write the single characters to the output:

    Blah b

Now, we encounter a back reference. Therefore, we need to go back 5 positions, and copying for L-amount of characters from the input to the output:

    Blah b                      [D=5, L=18]
    Blah bl                     [D=5, L=17]
    Blah bla                    [D=5, L=16]
    Blah blah                   [D=5, L=15]
    Blah blah_                  [D=5, L=14]
    Blah blah b                 [D=5, L=13]
    Blah blah bl                [D=5, L=12]
    Blah blah bla               [D=5, L=11]
    Blah blah blah              [D=5, L=10]
    Blah blah blah_             [D=5, L=9]
    Blah blah blah b            [D=5, L=8]
    Blah blah blah bl           [D=5, L=7]
    Blah blah blah bla          [D=5, L=6]
    Blah blah blah blah         [D=5, L=5]
    Blah blah blah blah_        [D=5, L=4]
    Blah blah blah blah b       [D=5, L=3]
    Blah blah blah blah bl      [D=5, L=2]
    Blah blah blah blah bla     [D=5, L=1]
    Blah blah blah blah blah    [D=5, L=0]
    Blah blah blah blah blah!
