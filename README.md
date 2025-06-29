<p align="center">
  <img src="./HSTU_Logo.png" alt="HSTU Logo" width="150">
</p>

<h2 align="center"><strong>Hajee Mohammad Danesh Science and Technology University</strong></h2>

<h3 align="center">Dinajpur-5200</h3>

---

<h2 align="center" style="color:#16a085;"><strong>📘 Course Information</strong></h2>

<p align="center">
  <strong>Course Title:</strong> Mathematical Analysis for Computer Science  
  <br>
  <strong>Course Code:</strong> CSE 361
</p>

---

<h2 align="center" style="color:#2980b9;"><strong>🧠 Algorithm Name</strong></h2>

<h1 align="center" style="color:#8e44ad;"><strong>🔐 GCP Cipher</strong></h1>

---

<h2 align="center" style="color:#16a085;"><strong>🧑‍💻 Submitted By</strong></h2>

<p align="center">
  <strong>Name:</strong> Md. Ridwanur Rahman Shuvo  
  <br>
  <strong>Student ID:</strong> 2102046  
  <br>
  <strong>Level:</strong> 3  
  <br>
  <strong>Semester:</strong> II  
  <br>
  <strong>Department:</strong> Computer Science and Engineering  
</p>

---

<h2 align="center" style="color:#16a085;"><strong>👨‍🏫 Submitted To</strong></h2>

<p align="center">
  <strong>Name:</strong> Pankaj Bhowmik  
  <br>
  <strong>Designation:</strong> Lecturer  
  <br>
  <strong>Department:</strong> Computer Science and Engineering  
</p>


---

# 🧠 Algorithm Description

## 🔐 Algorithm Name: **GCP Cipher**  
**(GCD-Controlled Position-based Cipher)**

This is a custom cryptographic algorithm based on:
- Character position in the string
- Multiplicative key (a prime number `a` such that gcd(a, 26) = 1)
- Modular arithmetic (mod 26 for the alphabet)
- Modular inverse for decryption

---


## 🔢 Table of Contents
- [🔐 Encryption Algorithm](#-encryption-algorithm)
- [🔓 Decryption Algorithm](#-decryption-algorithm)
- [🧪 Example Test Case](#-example-test-case)
- [📈 Flowcharts](#-flowcharts)
- [💻 Java Source Code](#-java-source-code)

---
# 🔐 Encryption Algorithm

Let:  
- `a` be a multiplicative key such that `gcd(a, 26) = 1`  
- `pos` = character position in plaintext (starting from 0)  
- `P[i]` =  index of the i-th plaintext character  
- `E[i]` = i-th character of ciphertext  

### Formula:
```text
E[i] = {a × (P[i] + pos)} mod 26

```
## 🔓 Decryption Algorithm

### Decryption Formula:
- `a⁻¹` = Modular inverse of `a` modulo 26  
- `E[i]` = i-th character of ciphertext 
- `pos` = Original position in plaintext  
- `D[i]`=Decrypted Message of E[i]

### Formula:
```text
D[i] = {(a⁻¹ × E[i]) - pos + 26} mod 26


```

---

## 🧪 Example Test Case

**Plaintext:** `HELLO`  
**Key (a):** 7 (coprime with 26)  
**Modular Inverse a⁻¹:** 15 (since 7 × 15 ≡ 1 mod 26)

### Step-by-step Encryption:

| Pos | Char | Index | Encrypted Index (E(x)) | Encrypted Char |
|-----|------|--------|------------------------|----------------|
| 0   | H    | 7      | {7× (7 +0)} % 26 = 23 | X              |
| 1   | E    | 4      | {7×(4+1)} % 26 = 9  | J              |
| 2   | L    | 11     | {7×(11+2)} % 26 = 13| N              |
| 3   | L    | 11     | {7×(11+3)} % 26 = 20| U             |
| 4   | O    | 14     | {7×(14+4)} % 26 = 22| W              |

🔐 **Ciphertext:** `XJNUW`

### Step-by-step Decryption:

| Pos | Char | Index | Decrypted Index (D(y)) | Decrypted Char |
|-----|------|--------|------------------------|----------------|
| 0   | X    | 23     | {(15×23)- 0 +26} %26 = 7| H              |
| 1   | J    | 9      | {(15×9)- 1 + 26} %26 = 4 | E              |
| 2   | N    | 13     | {(15×13)- 2 + 26} %26=11 | L              |
| 3   | U    | 20     | {(15×20)- 3 + 26} %26=11 | L              |
| 4   | W    | 22     | ({15×22)- 4 + 26} %26=14 | O              |

✅ **Decrypted Text:** `HELLO`


---

## Flowcharts









## 💻 Java Source Code

```java
public class GCPCipher {

    static int modInverse(int a, int m) {
        for (int x = 1; x < m; x++) {
            if ((a * x) % m == 1) return x;
        }
        return -1;
    }

    static int charToIndex(char c) {
        return c - 'A';
    }

    static char indexToChar(int i) {
        return (char) ('A' + i);
    }

    static String encrypt(String plaintext, int a) {
        StringBuilder ciphertext = new StringBuilder();
        plaintext = plaintext.toUpperCase();
        for (int i = 0; i < plaintext.length(); i++) {
            int index = charToIndex(plaintext.charAt(i));
            int cipherIndex = (a * (index + i + 26)) % 26;
            ciphertext.append(indexToChar(cipherIndex));
        }
        return ciphertext.toString();
    }

    static String decrypt(String ciphertext, int a) {
        StringBuilder plaintext = new StringBuilder();
        int a_inv = modInverse(a, 26);
        for (int i = 0; i < ciphertext.length(); i++) {
            int index = charToIndex(ciphertext.charAt(i));
            int plainIndex = (a_inv * index - i + 52) % 26;
            plaintext.append(indexToChar(plainIndex));
        }
        return plaintext.toString();
    }

    public static void main(String[] args) {
        String text = "HELLO";
        int key = 7;
        String encrypted = encrypt(text, key);
        String decrypted = decrypt(encrypted, key);
        System.out.println("Original: " + text);
        System.out.println("Encrypted: " + encrypted);
        System.out.println("Decrypted: " + decrypted);
    }
}


