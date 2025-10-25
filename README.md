# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:
~~~
#include <stdio.h>
#include <math.h>

int mod_exp(int base, int exp, int mod) {
    int result = 1;
    for (int i = 0; i < exp; i++) {
        result = (result * base) % mod;
    }
    return result;
}

int main() {
    int p, g, x, y, k, m, c1, c2, m_decrypted;

    printf("Enter a prime number p: ");
    scanf("%d", &p);

    printf("Enter primitive root g: ");
    scanf("%d", &g);

    printf("Enter private key x (1 < x < p-1): ");
    scanf("%d", &x);

    y = mod_exp(g, x, p);
    printf("Public key (y): %d\n", y);

    printf("\nEnter message (m < p): ");
    scanf("%d", &m);

    printf("Enter random key k (1 < k < p-1): ");
    scanf("%d", &k);

    c1 = mod_exp(g, k, p);
    c2 = (m * mod_exp(y, k, p)) % p;

    printf("\nCiphertext: (c1, c2) = (%d, %d)\n", c1, c2);

    int s = mod_exp(c1, x, p);
    int s_inverse = mod_exp(s, p - 2, p); 
    m_decrypted = (c2 * s_inverse) % p;

    printf("Decrypted message: %d\n", m_decrypted);

    return 0;
}
~~~


## Output:
<img width="592" height="287" alt="image" src="https://github.com/user-attachments/assets/dbe33e82-1fa6-4e89-a4c6-dc0bf7c42c18" />



## Result:
The program is executed successfully.
