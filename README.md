# Module-2 Part-2 (Introduction to Modern Cryptography)

## XOR
XOR is basically a bitwise operator.It takes two numbers as operands and does XOR on every bit of two numbers. The result of XOR is 1 if the two bits are different and 0 if they are same. <br />
0 ⊕ 0 = 0 <br />
1 ⊕ 0 = 1 <br />
0 ⊕ 1 = 1 <br />
1 ⊕ 1 = 0 <br />
**Example:** 73 ⊕ 87 = 1001001 ⊕ 1010111= 0011110 = 30 <br />

<details>
<summary> <strong>EXERCISE:</strong> Given an array find out the only element that occurs exactly once if every element other than the unique element occurs twice. </summary>
<strong>ANSWER:</strong> https://betterexplained.com/articles/swap-two-variables-using-xor/
</details>

Bitwise operators(XOR, AND, OR) can also be used on images (eg. using gmic or python PIL). <br />
- https://www.khanacademy.org/computing/computer-science/cryptography/ciphers/a/xor-and-the-one-time-pad


## One-Time Pad (OTP)
It is a method of encrypting plain text.
The two requirements for the One-Time pad are:
1. The key should be randomly generated as long as the length of the message.
2. The key is to be used to encrypt and decrypt a single message and then it is discarded.
So to encrypt every new message requires a new key of the same length.
- https://www.hypr.com/one-time-pad/

# Number Theory
Refer to the following link for a "cheat-sheet" of sorts: https://docs.google.com/document/d/1JZ2CAi6zfqTr-vIw1voUYhbvDNhK3RNF/edit?usp=sharing&ouid=108053057768377721012&rtpof=true&sd=true <br /> 

- https://www.nku.edu/~christensen/the%20mathematics%20of%20the%20RSA%20cryptosystem.pdf


# RSA
1. Select 2 large prime numbers,say p and q. You must be wondering why we are supposed to take large prime numbers. Be patient, I will tell you later.
2. Now take n=p*q
3. Φ(n)=(p-1)*(q-1)
4. Choose value of e such that 1<e<Φ(n) and gcd(Φ(n),e)=1.
5. Now,calculate d such that (e*d)%Φ(n)=1.
6. Public Key=(e,n); Private Key=(d,n)

Suppose we wanna encrypt a message M. <br />
C = M^e%n <br />
Now decryption will be in similar manner but using private key <br />
M = C^d%n <br />
Now coming to the question why we are spposed to take large prime numbers. You guessed it right that is it is based on difficulty of factoring large integers. <br />
You can refer: https://www.di-mgt.com.au/rsa_alg.html#encryption to read more about it. <br />
One of the flaws that you might feel is present in RSA is that given n, we would just "factor" it to get p,q! The truth is,
however factoring algorithms are SLOW. Given no specific property of n, the faster algorithm is Shor's algorithm which is a quantum 
algorithm. However, if n satisfies certain special properties (which varies with factoring algorithm), it can be factored very fast.
So if you're reluctant, your best bet is to just spam all the factoring algorithms and hope one of them works! <br />
To get a good summary, check out https://stackoverflow.com/questions/2267146/what-is-the-fastest-integer-factorization-algorithm <br />
You will find many different attacks on RSA which also exploit e or ciphertext given certain cases. <br />
To get a good list of attacks, check out https://github.com/RsaCtfTool/RsaCtfTool <br />

Challenges:
- https://cryptohack.org/challenges/
- https://cryptopals.com/
- https://play.picoctf.org/

Cryptography walkthroughs: https://www.youtube.com/playlist?list=PL1H1sBF1VAKU05UWhDDwl38CV4CIk7RLJ (there are many videos on RSA in computerphile)
