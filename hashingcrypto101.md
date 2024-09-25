# Hashing Crypto 101

Encryption and encoding are both techniques used to transform data, but they serve different purposes and operate differently. Here's a breakdown of their key differences:

### 1. **Purpose:**
   - **Encryption:** The primary purpose of encryption is **confidentiality**. It ensures that only authorized parties can read the data by converting it into a form that is unreadable without a specific decryption key.
   - **Encoding:** Encoding's purpose is **data representation** and **compatibility**. It transforms data into a specific format so that it can be properly processed, transmitted, or stored by different systems.

### 2. **Reversibility:**
   - **Encryption:** Encryption is **reversible** but requires a decryption key. The data can only be reverted to its original form by someone who possesses the correct key.
   - **Encoding:** Encoding is also **reversible**, but it does not require a key. Anyone with knowledge of the encoding scheme can decode the data back to its original form.

### 3. **Security:**
   - **Encryption:** Encryption is designed with security in mind. The goal is to protect data from unauthorized access. Strong encryption algorithms are difficult to break without the correct key.
   - **Encoding:** Encoding is not meant for security. It does not protect data from being read by unauthorized parties, as the encoding schemes are usually well-known and easy to reverse.

### 4. **Examples:**
   - **Encryption:**
     - **AES (Advanced Encryption Standard):** Symmetric encryption algorithm used widely for securing data.
     - **RSA:** Asymmetric encryption algorithm used for securing data transmission.
   - **Encoding:**
     - **Base64:** Common encoding scheme used to represent binary data in an ASCII string format.
     - **ASCII (American Standard Code for Information Interchange):** Encoding scheme that represents text in computers.

### 5. **Use Cases:**
   - **Encryption:**
     - Securing communication over the internet (e.g., HTTPS).
     - Protecting sensitive data such as passwords, financial information, or personal details.
   - **Encoding:**
     - Ensuring data can be safely transmitted over protocols that only support text.
     - Converting data into a format that can be read by different systems (e.g., UTF-8 for text encoding).

### 6. **Data Integrity:**
   - **Encryption:** Encryption typically focuses on confidentiality rather than data integrity. However, some encryption schemes include mechanisms to ensure the integrity and authenticity of the data (e.g., authenticated encryption).
   - **Encoding:** Encoding does not ensure data integrity. If the encoded data is altered, the decoding process will produce incorrect or corrupted output.

### 7. **Transformation Process:**
   - **Encryption:** The process involves using an encryption algorithm and a key to transform the data. Without the correct key, the data remains unintelligible.
   - **Encoding:** The process involves using a known algorithm to convert data into another format. The encoding and decoding processes are usually straightforward and do not require any secret information.

### Summary
- **Encryption**: Focuses on data security and requires a key to reverse.
- **Encoding**: Focuses on data representation and compatibility, and does not involve security.

In practice, encryption is used to protect data from unauthorized access, while encoding is used to ensure that data can be correctly processed and interpreted by different systems.



#### Hash Collision
2 different inputs with same output
Pigeonhole effect = if there are a set number of different output values foir the hash function, but you can give it any size input. As there are more inputs than output, some of the inputs must give same output.


#### Uses for hashing
- encrypting passowrds is a bad idea as the key neds to be stored somewehre.

#### Recognizing password hashes
- prefix tells hte hashing algorithmused
- ![image](https://github.com/user-attachments/assets/e9aa8165-80d6-450e-b196-14e657d4a8b1)

- ![image](https://github.com/user-attachments/assets/8be6d64b-9132-44a5-a520-15fc08c7dcda)

- ![image](https://github.com/user-attachments/assets/40896a0f-000d-4980-8dd6-20eca7cbe11f)


