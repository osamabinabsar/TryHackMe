# Cryptography



### Ceaser Cipher
- Substitution
- Transposition

#### In mathematical terms, we need a hard problem, i.e., a problem that cannot be solved in polynomial time. A problem that we can solve in polynomial time is a problem that’s feasible to solve even for large input, although it might take the computer quite some time to finish.


**Cryptographic Algorithm or Cipher:** This algorithm defines the encryption and decryption processes.
**Key:** The cryptographic algorithm needs a key to convert the plaintext into ciphertext and vice versa.
**plaintext** is the original message that we want to encrypt
**ciphertext** is the message in its encrypted form

#### DES is symmetric encryption algorithm

### AES
 AES repeats the following four transformations multiple times:

    SubBytes(state): This transformation looks up each byte in a given substitution table (S-box) and substitutes it with the respective value. The state is 16 bytes, i.e., 128 bits, saved in a 4 by 4 array.
    ShiftRows(state): The second row is shifted by one place, the third row is shifted by two places, and the fourth row is shifted by three places. This is shown in the figure below.
    MixColumns(state): Each column is multiplied by a fixed matrix (4 by 4 array).
    AddRoundKey(state): A round key is added to the state using the XOR operation.

Illustration of the ShiftRows function when applied on a four by four array
![049bad7deb4e6dd426335d7c3477f10a](https://github.com/user-attachments/assets/00465596-815e-42ab-81c4-88b8e99e6c0f)


The total number of transformation rounds depends on the key size.

![image](https://github.com/user-attachments/assets/1029c000-01eb-425b-8f36-46cee798a29c)

### Assymmetric Encryption
- GNUPG
- OpenSSL

  ASCII armoured output, which can be opened in any text editor, you should add the option --armor. For example, gpg --armor --symmetric --cipher-algo CIPHER message.txt

### RSA
Uses complex math 
Available through programs and programming libraries

![image](https://github.com/user-attachments/assets/075a9804-d678-441f-8978-93dae7e0ab83)



### Hashing
A cryptographic hash function is an algorithm that takes data of arbitrary size as its input and returns a fixed size value, called message digest or checksum, as its output. For example, sha256sum calculates the SHA256 (Secure Hash Algorithm 256) message digest. SHA256, as the name indicates, returns a checksum of size 256 bits (32 bytes). This checksum is usually written using hexadecimal digits. Knowing that a hexadecimal digit represents 4 bits, the 256 bits checksum can be represented as 64 hexadecimal digits.

**HMAC**

Hash-based message authentication code (HMAC) is a message authentication code (MAC) that uses a cryptographic key in addition to a hash function.

According to RFC2104, HMAC needs:

secret key
inner pad (ipad) a constant string. (RFC2104 uses the byte 0x36 repeated B times. The value of B depends on the chosen hash function.)
outer pad (opad) a constant string. (RFC2104 uses the byte 0x5C repeated B times.)

Calculating the HMAC follows the following steps as shown in the figure:

Append zeroes to the key to make it of length B, i.e., to make its length match that of the ipad.
Using bitwise exclusive-OR (XOR), represented by ⊕, calculate key ⊕ ipad.
Append the message to the XOR output from step 2.
Apply the hash function to the resulting stream of bytes (in step 3).
Using XOR, calculate key ⊕ opad.
Append the hash function output from step 4 to the XOR output from step 5.
Apply the hash function to the resulting stream of bytes (in step 6) to get the HMAC.


### PKI & SSL/TLS



For a certificate to get signed by a certificate authority, we need to:

1. Generate Certificate Signing Request (CSR): You create a certificate and send your public key to be signed by a third party.
2. Send your CSR to a Certificate Authority (CA): The purpose is for the CA to sign your certificate. The alternative and usually insecure solution would be to self-sign your certificate.


 You can use openssl to generate a certificate signing request using the command openssl req -new -nodes -newkey rsa:4096 -keyout key.pem -out cert.csr. We used the following options:

    req -new create a new certificate signing request
    -nodes save private key without a passphrase
    -newkey generate a new private key
    rsa:4096 generate an RSA key of size 4096 bits
    -keyout specify where to save the key
    -out save the certificate signing request
  The -x509 indicates that we want to generate a self-signed certificate instead of a certificate request. The -sha256 specifies the use of the SHA-256 digest. It will be valid for one year as we added -days 365.


### Authenticating with Passwords


