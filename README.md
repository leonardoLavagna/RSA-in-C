# RSA-in-C
A simple implementation of the standard RSA algorithm for asymmetric key cryptography. Note that this implementation is secure, but the protocol one uses can be insecure. In particular it is possible to carry out the following Chosen Chipertext Attack against RSA (which is an attack against the protocol and not against the standard algorithm):
- An evesdropper $E$ monitoring the comunication between $A$ and $B$ manages to get a ciphertext $c$;
- $E$ would like to recover the message $m=c^d$ where $d$ is the (hard) inverse of the public key $e$ of $A$ (mod(n=(p-1)(q-1))$ as in the standard RSA algorithm); 
- To recover $m$ choose a random number $r < n$, get the public key $e$ and compute $x=r^e mod(n)$;
- Compute $y=xc mod(n)$ and $t=r^{-1} mod(n)$;
- If $x=r^e mod(n)$, then $r=x^d mod(n)$;
- At this point $E$ gets $A$ to sign $y$ with the private key, thereby decrypting $y$ so $E$ recieves from $A$ the message $u=y^d mod(n)$;
- $E$ computes $tu mod(n)$ which is exactly the message $m$.

The point here is that $A$ signs the message and not the hash of the message. The weakness all these kinds of attacks have use is that exponentiation preserves the multiplicative structure of the input. There is another more subtle weakness: most algorithms to find large primes $p$ and $q$ are probabilistic, what will happen if $p$ and $q$ are tought to be prime but are indeed compisite? In this case most of the time encryption and decryption won't work properly and you can notice right away. There are a few numbers, though, the Carmichael numbers, which certain probabilistic primality algorithms will fail to detect. 

### What's in here?
Here you can find the standard implementation in C of the RSA algorithm. To execute the code either run it online, e.g. here: https://onlinegdb.com/sjXC-t22a or use the command line, typically the following commands should work: 
- `gcc -<programName>.c` wich will compile the file `<programName.c>` and produce the output file `a.out`
- `./a wich will execute the code obtained in the previous point.
