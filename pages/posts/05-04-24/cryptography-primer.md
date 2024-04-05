Since we recently noticed some confusion, even among industry professionals, we decided to write a brief primer on the most well-known *cryptographic algorithms* and their applications:  

- 𝐀𝐄𝐒 (𝐀𝐝𝐯𝐚𝐧𝐜𝐞𝐝 𝐄𝐧𝐜𝐫𝐲𝐩𝐭𝐢𝐨𝐧 𝐒𝐭𝐚𝐧𝐝𝐚𝐫𝐝): AES is a symmetric key algorithm that operates on blocks of data, using key sizes of 128, 192, or 256 bits.  
AES is widely adopted for encrypting data at rest in databases and storage systems.  

- 𝐑𝐒𝐀 (𝐑𝐢𝐯𝐞𝐬𝐭-𝐒𝐡𝐚𝐦𝐢𝐫-𝐀𝐝𝐥𝐞𝐦𝐚𝐧): RSA is an asymmetric key algorithm that uses a pair of public and private keys.  
The security is based on the difficulty of factoring large composite numbers.  
Commonly used for securing communication channels (e.g., HTTPS), digital signatures for data integrity verification, and key exchange protocols.  

- 𝐄𝐥𝐥𝐢𝐩𝐭𝐢𝐜 𝐂𝐮𝐫𝐯𝐞 𝐂𝐫𝐲𝐩𝐭𝐨𝐠𝐫𝐚𝐩𝐡𝐲 (𝐄𝐂𝐂): ECC relies on the mathematical properties of elliptic curves over finite fields for secure key exchange and digital signatures.  
Efficiently used in communication protocols (e.g., TLS, HTTPS) for key exchange and data integrity verification.  
Also suitable for resource-constrained environments like IoT devices.  

- 𝐒𝐇𝐀-256 (𝐒𝐞𝐜𝐮𝐫𝐞 𝐇𝐚𝐬𝐡 𝐀𝐥𝐠𝐨𝐫𝐢𝐭𝐡𝐦 256-𝐛𝐢𝐭): SHA-256 is a cryptographic hash function that produces a fixed-size output (256 bits).  
Primarily employed for ensuring data integrity, creating digital signatures, compute digital forensics fingerprints and ensure efficient comparison of files.  

- 𝐀𝐫𝐠𝐨𝐧2: Argon2 is a key derivation function specifically designed for hashing passwords.  
It is resistant to GPU and ASIC attacks and provides a high level of security.  
Primarily used for securely hashing passwords in applications where user credentials are stored.  