_[<<< Return to BitsCTF 2017 tasks and writeups](/bitsctf-2017)_
# Sherlock (Crypto, 60 points)

>Sherlock has a mystery in front of him. Help him to find the flag.

This challenge is [an extract](final.txt) from the adventures of Sherlock Holmes. While I was reading the first paragraph, a thing really jumped out at me: there were some capital letters randomly put in the text, such as "i was seiZEd with a keen desiRe tO see holmes again".

Then I extracted all the capital letters, which eventually gave "binary words" (ZERO and ONE).

```python
>>> file = open('final.txt', 'r').read()
>>> capitals = ''.join([c for c in file if c.isupper()])
>>> print capitals
ZEROONEZEROZEROZEROZEROONEZEROZEROONEZEROZEROONEZEROZEROONEZEROONEZEROONEZEROONE
ZEROZEROZEROONEZEROONEZEROZEROONEONEZEROONEZEROZEROZEROZEROONEONEZEROONEZEROONEZERO
ONEZEROZEROZEROONEZEROZEROZEROONEONEZEROZEROONEONEONEONEZEROONEONEZEROONEONEZEROONE
ZEROZEROZEROZEROZEROONEONEZEROZEROZEROONEZEROONEONEZEROZEROONEZEROZEROZEROZEROONE
ONEZEROZEROONEONEZEROONEZEROONEONEONEONEONEZEROZEROONEONEZEROZEROZEROONEZEROONEONE
ZEROONEONEONEZEROZEROONEZEROONEONEONEONEONEZEROONEONEONEZEROZEROZEROZEROZEROONEONE
ZEROONEONEZEROZEROZEROZEROONEONEZEROONEZEROZEROZEROZEROONEONEZEROZEROZEROONEZEROONE
ONEZEROONEONEONEZEROZEROONEZEROONEONEONEONEONEZEROZEROONEONEZEROONEZEROONEZEROZERO
ONEONEZEROZEROZEROONEZEROZEROONEONEZEROONEONEONEZEROZEROONEONEZEROZEROONEONEZEROONE
ONEONEONEONEZEROONE
>>>
```

Then I turned these ZERO and ONE into binary, and converted it in ASCII.

```python
>>> binary = capitals.replace('ZERO', '0').replace('ONE', '1')
>>> print binary
01000010010010010101010001010011010000110101010001000110011110110110100000110001011
00100001100110101111100110001011011100101111101110000011011000011010000110001011011
10010111110011010100110001001101110011001101111101
>>> binary = int(binary, 2)
>>> print binary
27268660991179512954985252255578187377187154666285848717059109757
>>> binascii.unhexlify('%x' % binary)
'BITSCTF{h1d3_1n_pl41n_5173}'
```