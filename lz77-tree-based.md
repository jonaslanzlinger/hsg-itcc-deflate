# LZ77 - tree based implementation

There are multiple approaches on how the LZ77 matching mechanism can be implemented.

In [this repository](https://github.com/cstdvd/lz77), you can find a very nice C-implementation that implemented the matching between the sliding window and the lookahead buffer through a binary tree, stored in an array.

## Usage

1. Clone the repository locally.

       git clone https://github.com/cstdvd/lz77

3. Navigate into the root directory of the repository.

       cd lz77

5. You can execute the "make" command to build the project files.

       make

7. Create a simple textfile for the input, and another textfile for the output. Write some text inside the input file and leave the output file empty.

8. Run the compression on the input file.

       ./lz77 -c -i <inputfile> -o <outputfile>

## Comments

Simply executing the program might not be very interesting. Here are some things that you might want to explore further in the code:
* The matching is done via a binary tree. Investigate the methods in the "tree.c" file.
* If you want to know how the internal representation of the tree looks like, you can add the following line at line 137:

      printtree(tree, root);
  
What you see at the output then is the binary tree offset values of each node at the end of the compression process. Maybe modify in file "tree.c" line 276:

    printf("offset: %d, length: %d\n", tree[root].off, tree[root].len);
  
* Investigate how the file "lz77.c" is structured, and how it interacts with the following components:
  * File I/O
  * Binary trees
