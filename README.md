# breaksub
Python implementation of a Markov Chain Monte Carlo method for breaking monoalphabetic substitution ciphers. 

## prerequisites
<li>Python 3.7+ should work</li>
<li>The only dependency is the `tqdm` module which is optional (can be disabled with the `--no-progress` option)</li>

## options
<li>--iters: Number of iterations of Monte Carlo method. Default is 5000</li>
<li>--no-progress: Do not show progress bar. If not specified, `tqdm` module must be installed</li>
<li>--alphabet: Comma separated file containing the alphabet. Default is lowercase English alphabet with period(".") and space(" ")</li>
<li>--letter-probs: Comma separated file containing the probability of occurrence of each letter. If not provided, reasonable default values are used for the default alphabet</li>
<li>--transition-probs: Comma separated file where the j-th number of i-th line is the probability of occurrence of j-th character right after i-th character of the alphabet. If not provided, reasonable default values are used for the default alphabet</li>

It is assumed that input ciphertext consists of characters from the specified alphabet.

## usage
use default alphabet with default parameters
```bash
./breaksub.py test_data/ciphertext_russel.txt > russel.txt
```

do 3000 iterations of the method (default is 5000) and do not show progress bar
```bash
./breaksub.py test_data/ciphertext_warandpeace.txt --no-progress --iters 3000 > warandpeace.txt
```

specifying alphabet and algorithm parameters
```bash
./breaksub.py --alphabet example_options/alphabet.csv --letter-probs example_options/letter_probabilities.csv --transition-probs example_options/letter_transition_matrix.csv --iters 7000 test_data/ciphertext_paradiselost.txt > paradiselost.txt
```


```py
from breaksub import *

with open("test_data/ciphertext_warandpeace.txt") as f:
    ciphertext = f.read()

alphabet = default_alphabet() # a-z, space, period
ciphertext = [c for c in ciphertext if c in alphabet] # remove characters that are not in our alphabet

options = DecipherOptions(iters=4000, print_progress=True)
cipher = substitution_decipher(ciphertext, options) # break the cipher
print('cipher is ', cipher)

plaintext = recover_plaintext(cipher, ciphertext) # recover plaintext given the cipher
print(plaintext)
```

## notes
<li>The algorithm is probabilistic so it does not always converge to the optimal solution. Try running it multiple times if the output does not make sense.</li>
<li>The algorithm does not work well if input is too short</li>
