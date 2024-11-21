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