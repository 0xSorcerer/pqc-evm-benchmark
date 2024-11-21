# Lamport OTS

Lamport One-Time Signatures (OTS) are considered to be **quantum-resistant** because they solely rely on cryptographic hash functions, which are fundamentally different from the mathematical problems underpinning traditional cryptographic algorithms like ECDSA or RSA. 

#### Key points of Quantum Resistance

1. **Hash Functions Are Resistant to Shor's Algorithm**
	- Shor's algorithm, the primary quantum algorithm for breaking classical cryptography, is effective against problems like:
		- Integer factorization (RSA).
		- Discrete logarithms (ECDSA -> EVM)
	- However, Shor's algorithm cannot efficiently attack cryptographic hash functions because hash functions are not based on mathematical structures like factorization or discrete logarithms. 
2. **Grover's Algorithm for Hash Functions**
	- Grover's algorithm allows quantum computers to search unstructured spaces (i.e., all possible hash outputs) in $\sqrt{N}$ time where $N$ is the number of possibilities.
	- For a cryptographic hash function with a 256-bit output (like Keccak-256 used in EVM):
		- Classical brute force attack require $2^{256}$ operations to find a preimage.
		- Quantum attack via Grover's algorithm require $\sqrt{2^{256}} = 2^{128}$ operations.
3. **Lamport OTS Relies Only on Hash Function Security**
	- Lamport signatures depend only on the preimage resistance of hash functions. 

## Lamport OTS Algorithm

### Private Key Generation
The private key consists of $2n$ random values, where $n$ is the length of the hash output in bits. Each random value is a random string of bits (e.g., 256 bits if using Keccak-256).
#### Algorithm
1. Generate $n$ random bitstrings for the "0" part (first half) of the private key: $SK_0 = \{sk_{0, 1}, sk_{0, 2}, \dots, sk_{0, n}\}$
2. Generate $n$ random bitstrings for the "1" part (second half) of the private key: $SK_1 = \{sk_{1, 1}, sk_{1, 2}, \dots, sk_{1, n}\}$
#### Output
The private key $SK = (SK_0, SK_1)$ where $SK = \{(sk_{0, 1}, sk_{1, 1}), (sk_{0, 2}, sk_{1, 2}), \dots , (sk_{0, n}, sk_{1, n}) \}$

### Public Key Generation
The public key is derived by applying a hash function $H$ to each component of the private key.
#### Algorithm
1. Compute the public key $PK$ as
	- $PK_0 = \{H(sk_{0, 1}), H(sk_{0, 2}), \dots , H(sk_{0, n}) \}$
	- $PK_1 = \{H(sk_{1, 1}), H(sk_{1, 2}), \dots , H(sk_{1, n}) \}$
2. Combine $PK_0$ and $PK_1$ into the final public key: $PK = (PK_0, PK_1)$
#### Output
The public key $PK = \{(H(sk_{0, 1}), H(sk_{1, 1})), (H(sk_{0, 2}), H(sk_{1, 2})), \dots , (H(sk_{0, n}), H(sk_{1, n})) \}$
$PK  = \{(pk_{0, 1}, pk_{1, 1}), (pk_{0, 2}, pk_{1, 2}), \dots , (pk_{0, n}, pk_{1, n}) \}$

