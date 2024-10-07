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
