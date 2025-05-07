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
```
#include <stdio.h>
#include <math.h>

// Function to calculate (base^exp) % mod
long long mod_pow(long long base, long long exp, long long mod) {
    long long result = 1;
    base = base % mod;

    while (exp > 0) {
        if (exp % 2 == 1)
            result = (result * base) % mod;

        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

// Modular inverse using Fermat's Little Theorem
long long modinv(long long a, long long p) {
    return mod_pow(a, p - 2, p);
}

int main() {
    long long p, g, x, y, k, m, c1, c2, s, decrypted;

    // Key Generation
    printf("Enter a large prime number (p): ");
    scanf("%lld", &p);

    printf("Enter primitive root modulo p (g): ");
    scanf("%lld", &g);

    printf("Enter private key (x): ");
    scanf("%lld", &x);

    y = mod_pow(g, x, p);
    printf("Public key (p, g, y): (%lld, %lld, %lld)\n", p, g, y);

    // Encryption
    printf("\n--- Encryption ---\n");
    printf("Enter message (m): ");
    scanf("%lld", &m);

    printf("Enter random integer (k): ");
    scanf("%lld", &k);

    c1 = mod_pow(g, k, p);
    c2 = (m * mod_pow(y, k, p)) % p;

    printf("Ciphertext: (c1, c2) = (%lld, %lld)\n", c1, c2);

    // Decryption
    printf("\n--- Decryption ---\n");
    s = mod_pow(c1, x, p);
    decrypted = (c2 * modinv(s, p)) % p;

    printf("Decrypted message: %lld\n", decrypted);

    return 0;
}

```

## Output:
![1](https://github.com/user-attachments/assets/7027eb00-fcfd-4480-9a4f-bd1d52fe8cf4)


## Result:
The program is executed successfully.
