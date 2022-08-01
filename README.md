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

![meme](https://user-images.githubusercontent.com/99350017/182178600-2d4e30e3-7fb3-4e93-998b-138c7cc20845.jpg)



Trying to formulate an attack for the scheme will often result in a compute-intensive problem. Of course, given enough computation power 
and time, you can technically break all the algorithms. 
However, there are many cases that the data can be found fast and in an appreciable time, mostly owing to people chosing 
vulnerable numbers.
So yes, given any compute-intensive problem, you can even frame your own scheme!

![diffie hellman,one of the first public-key protocols](https://user-images.githubusercontent.com/99350017/182178671-78faec75-50e0-40bd-947d-e352ccf14faf.png)


(example of Diffie–Hellman key exchange, one of the first public-key protocols)

## XOR
During any programming course, you must've come through the following logical operators:(using C++ synthax)<br/>
- AND `a && b`
- OR `a || b` 
- NOT `!a`


Note that these operators worked with groups of bytes and gave a boolean output.

<img width="1045" alt="truth-table" src="https://user-images.githubusercontent.com/99350017/182178803-465be571-12f9-4ef8-ad7d-7b6942d7609b.png">

Now, there is something called 'bitwise operators' which work on the bits within the byte. The calculation performed on bits is just like that
of logical operators. They take inputs as an integer and return an integer. These are:
- AND `a & b`
- OR `a | b` 
- XOR `a ^ b`,
- Left Shift `a << b` 
- Right Shift `a >> b`
- One's Complement or NOT `~a`

XOR is one of the most useful operations in cryptography. It takes two numbers as operands and does XOR on every bit of two numbers. The result of XOR is 1 if the two bits are different and 0 if they are same (hence the name **Exclusive OR**). <br />


**Example:** 73 ⊕ 87 = (1001001)<sub>2</sub> ⊕ (1010111)<sub>2</sub>= (0011110)<sub>2</sub> = 30 <br />

XOR is both commutative and associative.

<details>
<summary> <strong>EXERCISE:</strong> Given an array find out the only element that occurs exactly once if every element other than the unique element occurs twice. </summary>
<strong>ANSWER : </strong> Just XOR all the elements of the array!
</details>
Since all the data is represented on modern storage media using the binary numeral system, you can perform bitwise operators over anything!


For example, images can be XORed using `gmic` or `PIL`. <br />

**Text Guides:**

- https://www.khanacademy.org/computing/computer-science/cryptography/ciphers/a/xor-and-the-one-time-pad
- https://betterexplained.com/articles/swap-two-variables-using-xor/


## One-Time Pad (OTP)
It is a method of encrypting plain text.
The two requirements for the One-Time pad are:
1. The key should be randomly generated as long as the length of the message.
2. The key is to be used to encrypt and decrypt a single message and then it is discarded.
So to encrypt every new message requires a new key of the same length.

**Text Guides:**
- https://www.hypr.com/one-time-pad/

# Number Theory
Refer to the following link for a "cheat-sheet" of sorts: https://docs.google.com/document/d/1JZ2CAi6zfqTr-vIw1voUYhbvDNhK3RNF/edit?usp=sharing&ouid=108053057768377721012&rtpof=true&sd=true <br /> 

**Text Guides:**
- https://www.nku.edu/~christensen/the%20mathematics%20of%20the%20RSA%20cryptosystem.pdf


# RSA
Ah, the star scheme of this week. **RSA** (Rivest–Shamir–Adleman) is a public-key cryptosystem that is widely used for secure data transmission. It is also one of the oldest. The acronym "RSA" comes from the surnames of Ron Rivest, Adi Shamir and Leonard Adleman, who publicly described the algorithm in 1977. There are so many resouces to learn it,but here's a small summary of the RSA scheme : 

1. Select 2 prime numbers,say p and q.
2. Now take n=p\*q
3. Calculate the totient function Φ(n)=(p-1)\*(q-1)
4. Choose value of e such that 1<e<Φ(n) and gcd(Φ(n),e)=1.
5. Now,calculate d such that (e\*d) mod Φ(n)=1.
6. Public Key=(e,n); Private Key=(d,n)

Suppose we wanna encrypt a message M. <br />
C = M^e mod n <br />
Now decryption will be in similar manner but using private key <br />
M = C^d mod n <br />

One of the flaws that you might feel is present in RSA is that given n, we would just "factor" it to get p,q! The truth is,
however factoring algorithms are SLOW. Given no specific property of n, the faster algorithm is Shor's algorithm which is a quantum 
algorithm. However, if n satisfies certain special properties (which varies with factoring algorithm), it can be factored very fast.
So if you're reluctant, your best bet is to just spam all the factoring algorithms and hope one of them works! <br />
To get a good summary, check out https://stackoverflow.com/questions/2267146/what-is-the-fastest-integer-factorization-algorithm <br />
You will find many different attacks on RSA which also exploit e or ciphertext given certain cases. <br />
To get a good list of attacks, check out https://github.com/RsaCtfTool/RsaCtfTool <br />

However, in actual practise, the key sizes are 2,048 to 4,096 bit, refer https://crypto.stackexchange.com/questions/27575/why-isnt-a-table-used-to-solve-the-large-number-factoring-problem .

eg. you can see the public key of the website you're browsing in it's certificate.
**Text Guides:**
- https://www.di-mgt.com.au/rsa_alg.html#encryption

**Video Guides:**
- https://youtu.be/JD72Ry60eP4 (there are many videos on RSA and other schemes on computerphile)

**Practise:**
- https://cryptohack.org/challenges/
- https://cryptopals.com/
- https://play.picoctf.org/
- https://ctflearn.com/

**Cryptography walkthroughs:**
- https://www.youtube.com/playlist?list=PL1H1sBF1VAKU05UWhDDwl38CV4CIk7RLJ 
