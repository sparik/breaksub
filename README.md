# decipher_substitution
This repository contains a python script that uses a probabilistic Markov Chain Monte Carlo method to decrypt text encoded with a secret substitution cipher. 

## prerequisites
<li>Python 3.7+ should work</li>
<li>The only dependency is the `tqdm` module which is optional (can be disabled with the `--no-progress` option)</li>

## usage
use default alphabet with default parameters
```
./decipher_substitution.py test_data/ciphertext_russel.txt > plaintext_russel.txt
```

do 3000 iterations of the method (default is 5000) and do not show progress bar
```
./decipher_substitution.py test_data/ciphertext_russel.txt --no-progress --iters 3000 > plaintext_russel.txt
```

## options
<li>--iters: Number of iterations of Monte Carlo method. Default is 5000</li>
<li>--no-progress: Do not show progress bar. If not specified, `tqdm` module must be installed</li>
<li>--alphabet: Comma separated file containing the alphabet. Default is lowercase English alphabet with period(".") and space(" ")</li>
<li>--letter-probs: Comma separated file containing the probability of occurrence of each letter. If not provided, reasonable default values are used for the default alphabet</li>
<li>--transition-probs: Comma separated file where the j-th number of i-th line is the probability of occurrence of j-th character right after i-th character of the alphabet. If not provided, reasonable default values are used for the default alphabet</li>

It is assumed that input ciphertext consists of characters from the specified alphabet.

## notes
<li>The algorithm is probabilistic so it does not always converge to the optimal solution. Try running it multiplle times if the output does not make sense.</li>
<li>The algorithm does not work well if input is too short</li>
