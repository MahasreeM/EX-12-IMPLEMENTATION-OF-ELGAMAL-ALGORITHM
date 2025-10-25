## REG.NO:212224110035
## DATE:25-10-2025
## AIM:

To implement the ElGamal encryption and decryption algorithm using C for secure communication.


## ALGORITHM:
1.	Choose a large prime number p and a primitive root g of p.
2.	Select a private key x such that 1 < x < p.
3.	Compute the public key y = g^x mod p.
4.	To encrypt a message M:
a.	Choose a random integer k such that 1 < k < p.
b.	Compute C1 = g^k mod p.
c.	Compute C2 = (M * y^k) mod p.
d.	The ciphertext is the pair (C1, C2).
5.	To decrypt the ciphertext (C1, C2):
a.	Compute s = C1^(p-1-x) mod p.
b.	Compute the original message M = (C2 * s) mod p.
6.	Display the decrypted message.


## PROGRAM:
```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <time.h>


long long modPow(long long base, long long exp, long long mod) {
    long long result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1)
            result = (result * base) % mod;
        base = (base * base) % mod;
        exp /= 2;
    }
    return result;
}


long long modInverse(long long a, long long p) {
    return modPow(a, p - 2, p);
}

int main() {
    srand(time(NULL));

    
    long long p = 467;       
    long long g = 2;         
    long long x = rand() % (p - 2) + 1;  
    long long y = modPow(g, x, p);       

    printf("Public key (p, g, y): (%lld, %lld, %lld)\n", p, g, y);
    printf("Private key x: %lld\n", x);

    
    long long m; 
    printf("\nEnter a message (number < %lld): ", p);
    scanf("%lld", &m);

    long long k = rand() % (p - 2) + 1; 
    long long c1 = modPow(g, k, p);
    long long c2 = (m * modPow(y, k, p)) % p;

    printf("Ciphertext: (c1, c2) = (%lld, %lld)\n", c1, c2);

   
    long long s = modPow(c1, x, p);          
    long long m_decrypted = (c2 * modInverse(s, p)) % p;

    printf("Decrypted message: %lld\n", m_decrypted);

    return 0;
}
```
## OUTPUT:

<img width="647" height="271" alt="Screenshot 2025-10-25 132954" src="https://github.com/user-attachments/assets/41d36d63-b420-46c0-b18f-aa0cb160533d" />

## RESULT:
