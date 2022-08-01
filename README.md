# Module-2 Part-2 (Introduction to Modern Cryptography)
Welcome back to the Year of Security! This is Week 2 of Module 2 : Modern Cryptography.

Week 1 covered classical ciphers and different types of encodings (which, as stated, is not a cipher but very useful 
for describing data in different ways, specifically integers which can be then utilised in other encryption schemes). 
However, now you enter the realm of
modern cryptography. The schemes usually involve a series of mathematical steps to encrypt the data using key (or keys) to get
the ciphertext, which once received by the receiver, would have to go through another set of mathematical steps to get the data using same or 
different key 
depending on what type of
algorithm was used. (see https://en.wikipedia.org/wiki/Symmetric-key_algorithm and https://en.wikipedia.org/wiki/Public-key_cryptography).

One question comes to mind, how are these safe? After all, these are based on mathematics, and problems in mathematics get solved all the 
time!

![meme](https://i.imgflip.com/6okkmq.jpg)


Trying to formulate an attack for the scheme will often result in a compute-intensive problem. Of course, given enough computation power 
and time, you can technically break all the algorithms. 
However, there are many cases that the data can be found fast and in an appreciable time, mostly owing to people chosing 
vulnerable numbers.
So yes, given any compute-intensive problem, you can even frame your own scheme!

![example](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4c/Public_key_shared_secret.svg/375px-Public_key_shared_secret.svg.png)

(example of Diffie–Hellman key exchange, one of the first public-key protocols)

## XOR
During any programming course, you must've come through the following logical operators:AND(&&),OR(||) and NOT(!). Note that these operators
worked with groups of bytes and gave a boolean output.

![truth table](https://introcs.cs.princeton.edu/java/71boolean/images/truth-table.png)

Now, there is something called 'bitwise operators' which work on the bits within the byte. The calculation performed on bits is just like that
of logical operators. They take inputs as an integer and return an integer. These are AND &`OR(|), XOR(^), left shift(<<), right shift(>>) and
one's complement or NOT(~).
XOR is basically a bitwise operator.It takes two numbers as operands and does XOR on every bit of two numbers. The result of XOR is 1 if the two bits are different and 0 if they are same. <br />
0 ⊕ 0 = 0 <br />
1 ⊕ 0 = 1 <br />
0 ⊕ 1 = 1 <br />
1 ⊕ 1 = 0 <br />
**Example:** 73 ⊕ 87 = (1001001)<sub>2</sub> ⊕ (1010111)<sub>2</sub>= (0011110)<sub>2</sub> = 30 <br />

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
