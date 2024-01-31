---
title: 'Hash Function'
weight: 2
---

# Hash Function

If the input keys are integers, then simply returning key mod H_SIZE is generally a reasonable strategy, unless key happens to have some undesirable properties. In this case, the choice of hash function needs to be carefully considered. For instance, if the table size is 10 and the keys all end in zero, then the standard hash function is obviously a bad choice. For reasons we shall see later, and to avoid situations like the one above, it is usually a good idea to ensure that the table size is prime. When the input keys are random integers, then this function is not only very simple to compute but also distributes the keys evenly.

Usually, the keys are strings; in this case, the hash function needs to be chosen carefully.

One option is to add up the ASCII values of the characters in the string. In Figure 5.2 we declare the type INDEX, which is returned by the hash function. The routine in Figure 5.3 implements this strategy and uses the typical C method of stepping through a string.

The hash function depicted in Figure 5.3 is simple to implement and computes an answer quickly. However, if the table size is large, the function does not distribute the keys well. For instance, suppose that H_SIZE = 10,007 (10,007 is a prime number). Suppose all the keys are eight or fewer characters long. Since a char has an integer value that is always at most 127, the hash function can only assume values between 0 and 1016, which is 127 * 8. This is clearly not an equitable distribution!
```c
typedef unsigned int INDEX;
```
Figure 5.2 Type returned by hash function

 
```c
INDEX

hash(char *key, unsigned int H_SIZE)
{

unsigned int hash_val = 0;

/*1*/ while(*key != '\\0')

/*2*/ hash_val += *key++;

/*3*/ return(hash_val % H_SIZE);

}
```
Figure 5.3 A simple hash function

Another hash function is shown in Figure 5.4. This hash function assumes key has at least two characters plus the NULL terminator. 27 represents the number of letters in the English alphabet, plus the blank, and 729 is 272. This function only examines the first three characters, but if these are random, and the table size is 10,007, as before, then we would expect a reasonably equitable distribution. Unfortunately, English is not random. Although there are 263 = 17,576 possible combinations of three characters (ignoring blanks), a check of a reasonably large on-line dictionary reveals that the number of different combinations is actually only 2,851. Even if none of these combinations collide, only 28 percent of the table can actually be hashed to. Thus this function, although easily computable, is also not appropriate if the hash table is reasonably large.

Figure 5.5 shows a third attempt at a hash function. This hash function involves all characters in the key and can generally be expected to distribute well (it computes key/key_size - i - 1] 32i, and brings the result into proper range). The code computes a polynomial function (of 32) by use of Horner's rule.

For instance, another way of computing hk = k1 + 27k2 + 27 2k3 is by the formula hk = ((k3) * 27 + k2) * 27 + k1. Horner's rule extends this to an nth degree polynomial.

We have used 32 instead of 27, because multiplication by 32 is not really a multiplication, but amounts to bit-shifting by five. In line 2, the addition could be replaced with a bitwise exclusive or, for increased speed.

```c
INDEX

hash(char *key, unsigned int H_SIZE)
{

return ((key[0] + 27*key[1] + 729*key[2]) % H_SIZE);

}Figure 5.4 Another possible hash function -- not too good

INDEX

hash(char *key, unsigned int H_SIZE)
{

unsigned int hash_val = O;

/*1*/ while(*key != '\\0')

/*2*/ hash_val = (hash_val << 5) + *key++;

/*3*/ return(hash_val % H_SIZE);

}
```
Figure 5.5 A good hash function

The hash function described in Figure 5.5 is not necessarily the best with respect to table distribution, but does have the merit of extreme simplicity (and speed if overflows are allowed). If the keys are very long, the hash function will take too long to compute. Furthermore, the early characters will wind up being left-shifted out of the eventual answer. A common practice in this case is not to use all the characters. The length and properties of the keys would then influence the choice. For instance, the keys could be a complete street address. The hash function might include a couple of characters from the street address and perhaps a couple of characters from the city name and ZIP code. Some programmers implement their hash function by using only the characters in the odd spaces, with the idea that the time saved computing the hash function will make up for a slightly less evenly distributed function.

The main programming detail left is collision resolution. If, when inserting an element, it hashes to the same value as an already inserted element, then we have a collision and need to resolve it. There are several methods for dealing with this. We will discuss two of the simplest: open hashing and closed hashing.*

*These are also commonly known as separate chaining and open addressing, respectively.