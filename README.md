# homework 6: strings, searching, words

**Due date: Sunday, 22 May 2022, 11:59pm**

## introduction
In this homework, we are going to implement our own version of wordle, a
word-guessing game that has recently become popular. Next week we are going to
implement our own solver for the game, but this week we will build our own
playable version.

This is a "guess the secret word" kind of game. For each puzzle, there is a
particular secret 5-letter English word, and the player tries to infer what it
is by making a series of guesses. If the player can find the secret word, then
they win! And then they post some yellow and green squares on Twitter to amaze
their friends with their word-guessing prowess.

## Rules of the game

You may wish to give the game a try yourself to get a feel for it -- you can try
[the official version](https://www.nytimes.com/games/wordle/index.html), which
was recently acquired by the New York Times, or numerous unofficial clones
exist.

At each turn, the player guesses a word, which must come from a shared list of
5-letter English words. There is a dictionary of 5-letter words embedded in the
code for the game. Then the game compares the player's guess to the true secret
word, and returns a *response*, where the response consists of 5 colored
squares.

The squares have the following meaning:
  * gray: the corresponding letter does not appear in the secret word
  * yellow: the corresponding letter appears in the secret word, but not in that
    corresponding slot
  * green: the corresponding letter appears in the secret word, in that slot.

So each of these colors gives the player a lot of information about what the
secret word must be -- a gray square *means that a specific letter does not
appear at all in the secret word*, eliminating huge swaths of search space, and
yellow not only tells the player that a letter occurs in the secret word, but
that it *does not* occur in the corresponding slot.

Then it is up to the player to think of more words to try, until they find the
solution. We consider a guess to be *valid* when it is a 5-letter string of
ASCII characters a-z, and when it is one of the words in the specified word
list.


## Pieces to implement

The general shape of the program has been implemented for you, but some of the
functions have been replaced with stubs, which are for you to implement. There
are some explanatory comments, which should guide you on your path to building
your own wordle clone in C. These are all in `wordle_game.c`. You *may* also
need to change parts of `hw6.c` in order to make sure the game does not leak
memory.

## HARD MODE: warn the player when a guess is incompatible with the evidence
This part is completely optional. We will be impressed if you do it, but you do
not have to do it unless you feel like it. Doing a good job on this will get you
an extra credit point, for up to a 7/6 on the assignment.

You might notice that the game, as specified, allows the player to make *any*
valid guess, including those that are incompatible with the responses that have
been given for the previous guesses. If you do HARD MODE, tell the player "hey!
you can't make that guess, it's inconsistent with what I already told you!" (if
it is in fact inconsistent). For example, if you tell a player that there is no
letter 'm' in the word, but they guess a word containing an 'm', complain.

What information would you need to remember about each letter to accomplish
this?

## main function

For exercising our code, the main function (mostly written for you), will let
you play a game of wordle, once you finish the other functions!

You can execute the homework code like so, once everything is compiled:

```
./hw6
```

## Cleaning up our messes

For this homework, we are some dynamic data structures, with
`malloc`, `calloc`, and `realloc`.

**As part of your design**, you need to think about the dynamic data structures
that we are allocating, and come up with a plan for `free`-ing them. Which parts
of the code will allocate? How can you make sure every allocated pointer gets
`free`d?

In order to find out whether your code is cleaning up its messes, you should use
a tool called Valgrind.

If you have not yet installed Valgrind on your Linux system, you can install it
like so:
```
sudo apt install valgrind
```

You can run Valgrind to find out whether your program is leaking memory with the
following command:

```
valgrind --leak-check=full  ./hw6
```

Valgrind will then tell you whether you are successfully cleaning up all of the
allocated memory, or whether your program has leaks. You may find that
`valgrind` gives you more helpful output if you compile your code with `-g`.


## grading rubric
One point for a good design doc.

One point per each of the functions you need to implement in `wordle_game.c`.

One point for not leaking memory.

## deliverables

All of your deliverables for this homework should be checked in to a directory
called `hw6` in your CSE13s gitlab repository. Remember -- *add, commit, push*.

The resources you need are available in this directory.

  * By **Thursday, 19 May 2022**, you should have written your `DESIGN.md`,
    containing your thoughts and plans and pseudocode for this assignment.
  * `hw6.c` -- the `main`  function for the wordle game is in here. You'll need
    to make changes to this so that we don't leak memory.
  * `wordle_game.c` -- contains the new functions that you'll have to implement.
  * `wordle_game.h` -- declarations for your functions. You may want to add more
    declarations, in order to make sure we clean up all our memory.
  * Makefile -- make sure that you use the standard flags for the class in your
    Makefile.

## reading

You should read...
  * _The C Programming Language_ by Kernighan & Ritchie, Chapter 7 (to
    understand the I/O happening here).
  * _The C Programming Language_ by Kernighan & Ritchie, Chapter 8 (more
    discussion of I/O, also an explanation of realloc).
