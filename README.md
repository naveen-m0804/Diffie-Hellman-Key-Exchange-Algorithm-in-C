# Diffie-Hellman-Key-Exchange-Algorithm-in-C

### Aim:

To implement the Diffie-Hellman Key Exchange Algorithm in C, which allows two parties to securely exchange cryptographic keys over a public channel.

### Procedure: 

Understanding Diffie-Hellman:
The Diffie-Hellman Key Exchange is a method of securely exchanging cryptographic keys.
It allows two parties (say Alice and Bob) to generate a shared secret key without ever transmitting the secret itself over the communication channel.
Steps Involved:
Both Parties Agree on Public Parameters:
Choose a large prime number p.
Choose a generator g for the group of integers modulo p.
Key Generation:
Alice chooses a private key a and computes her public key A = g^a mod p.
Bob chooses a private key b and computes his public key B = g^b mod p.
Key Exchange:
Alice sends her public key A to Bob.
Bob sends his public key B to Alice.
Shared Secret Computation:
Alice computes the shared secret S = B^a mod p.
Bob computes the shared secret S = A^b mod p.
Both Alice and Bob now share the same secret S.

### Program:
```c
#include <stdio.h>
#include <math.h>

// Function to perform modular exponentiation
long long int powerMod(long long int base, long long int exp, long long int mod) {
    long long int result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

int main() {
    // Public parameters (prime number and primitive root)
    long long int p = 23; // Prime number
    long long int g = 5;  // Primitive root (generator)

    // Alice chooses a private key
    long long int a = 6;  // Private key for Alice
    // Alice computes her public key
    long long int A = powerMod(g, a, p);

    // Bob chooses a private key
    long long int b = 15;  // Private key for Bob
    // Bob computes his public key
    long long int B = powerMod(g, b, p);

    // Display public keys
    printf("Public parameters: (p = %lld, g = %lld)\n", p, g);
    printf("Alice's Public Key: %lld\n", A);
    printf("Bob's Public Key: %lld\n", B);

    // Alice computes the shared secret using Bob's public key
    long long int secret_Alice = powerMod(B, a, p);
    // Bob computes the shared secret using Alice's public key
    long long int secret_Bob = powerMod(A, b, p);

    // Display the shared secrets
    printf("Shared Secret computed by Alice: %lld\n", secret_Alice);
    printf("Shared Secret computed by Bob: %lld\n", secret_Bob);

    // The shared secret should be the same for both Alice and Bob
    if (secret_Alice == secret_Bob) {
        printf("Key Exchange Successful! Shared Secret: %lld\n", secret_Alice);
    } else {
        printf("Key Exchange Failed.\n");
    }

    return 0;
}
```

### OUTPUT:

```
Public parameters: (p = 23, g = 5)
Alice's Public Key: 8
Bob's Public Key: 19
Shared Secret computed by Alice: 2
Shared Secret computed by Bob: 2
Key Exchange Successful! Shared Secret: 2
```

### Result:

The Diffie-Hellman Key Exchange algorithm was successfully implemented in C. Both Alice and Bob computed the same shared secret, demonstrating secure key exchange over a public channel.
