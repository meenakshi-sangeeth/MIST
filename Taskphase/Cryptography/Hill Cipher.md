### Python script for Hill Cipher, Encryption and Decryption and an option to brute force it with known block size-(2x)

```
import numpy as np

key_matrix = np.zeros((2, 2), dtype=int)
message_vector = np.zeros((2, 1), dtype=int)
cipher_matrix = np.zeros((2, 1), dtype=int)

def get_key_matrix(key):
    k = 0
    for i in range(2):
        for j in range(2):
            key_matrix[i][j] = ord(key[k]) % 65
            k += 1

def encrypt_block(message_vector):
    for i in range(2):
        cipher_matrix[i][0] = 0
        for x in range(2):
            cipher_matrix[i][0] += (key_matrix[i][x] * message_vector[x][0])
        cipher_matrix[i][0] = cipher_matrix[i][0] % 26

def decrypt_block(cipher_vector, inv_key):
    plain_vector = np.zeros((2, 1), dtype=int)
    for i in range(2):
        plain_vector[i][0] = 0
        for x in range(2):
            plain_vector[i][0] += (inv_key[i][x] * cipher_vector[x][0])
        plain_vector[i][0] = plain_vector[i][0] % 26
    return plain_vector

def mod_inverse(a, m=26):
    for i in range(1, m):
        if (a * i) % m == 1:
            return i
    return None

def get_inverse_key():
    det = (key_matrix[0][0] * key_matrix[1][1] - key_matrix[0][1] * key_matrix[1][0]) % 26
    det_inv = mod_inverse(det)
    if det_inv is None:
        return None
    inv_key = np.zeros((2, 2), dtype=int)
    inv_key[0][0] = (key_matrix[1][1] * det_inv) % 26
    inv_key[0][1] = (-key_matrix[0][1] * det_inv) % 26
    inv_key[1][0] = (-key_matrix[1][0] * det_inv) % 26
    inv_key[1][1] = (key_matrix[0][0] * det_inv) % 26
    return inv_key

def hill_encrypt(message, key):
    get_key_matrix(key)
    if len(message) % 2 != 0:
        message += 'X'
    ciphertext = ""
    for i in range(0, len(message), 2):
        message_vector[0][0] = ord(message[i]) % 65
        message_vector[1][0] = ord(message[i+1]) % 65
        encrypt_block(message_vector)
        ciphertext += chr(cipher_matrix[0][0] + 65) + chr(cipher_matrix[1][0] + 65)
    return ciphertext

def hill_decrypt(ciphertext, key):
    get_key_matrix(key)
    inv_key = get_inverse_key()
    if inv_key is None:
        return "Error: Key not invertible"
    plaintext = ""
    for i in range(0, len(ciphertext), 2):
        cipher_vector = np.zeros((2, 1), dtype=int)
        cipher_vector[0][0] = ord(ciphertext[i]) % 65
        cipher_vector[1][0] = ord(ciphertext[i+1]) % 65
        plain_vector = decrypt_block(cipher_vector, inv_key)
        plaintext += chr(plain_vector[0][0] + 65) + chr(plain_vector[1][0] + 65)
    return plaintext

def brute_force(known_plain, known_cipher):
    if len(known_plain) < 4 or len(known_cipher) < 4:
        return None
    P = np.array([[ord(known_plain[0]) % 65, ord(known_plain[2]) % 65],
                  [ord(known_plain[1]) % 65, ord(known_plain[3]) % 65]])
    C = np.array([[ord(known_cipher[0]) % 65, ord(known_cipher[2]) % 65],
                  [ord(known_cipher[1]) % 65, ord(known_cipher[3]) % 65]])
    det = (P[0][0] * P[1][1] - P[0][1] * P[1][0]) % 26
    det_inv = mod_inverse(det)
    if det_inv is None:
        return None
    P_inv = np.array([[P[1][1] * det_inv % 26, -P[0][1] * det_inv % 26],
                      [-P[1][0] * det_inv % 26, P[0][0] * det_inv % 26]])
    K = np.dot(C, P_inv) % 26
    return K

print("1. Encrypt  2. Decrypt  3. Brute Force")
choice = input("Choice: ")

if choice == '1':
    message = input("Message: ").upper()
    key = input("Key (4 chars): ").upper()
    print("Ciphertext:", hill_encrypt(message, key))
elif choice == '2':
    ciphertext = input("Ciphertext: ").upper()
    key = input("Key (4 chars): ").upper()
    print("Plaintext:", hill_decrypt(ciphertext, key))
elif choice == '3':
    known_plain = input("Known plaintext (4+ chars): ").upper()
    known_cipher = input("Known ciphertext: ").upper()
    key = brute_force(known_plain, known_cipher)
    if key is not None:
        print("Key found:\n", key)
        full = input("Full ciphertext to decrypt: ").upper()
        if full:
            for i in range(2):
                for j in range(2):
                    key_matrix[i][j] = int(key[i][j])
            inv = get_inverse_key()
            plaintext = ""
            for i in range(0, len(full), 2):
                cv = np.zeros((2, 1), dtype=int)
                cv[0][0] = ord(full[i]) % 65
                cv[1][0] = ord(full[i+1]) % 65
                pv = decrypt_block(cv, inv)
                plaintext += chr(pv[0][0] + 65) + chr(pv[1][0] + 65)
            print("Decrypted:", plaintext)
    else:
        print("Key not found")
```
