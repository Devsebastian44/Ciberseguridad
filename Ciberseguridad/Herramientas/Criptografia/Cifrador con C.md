## Introducción al Cifrado de Archivos

El cifrado de archivos es una técnica fundamental para proteger información sensible.  
Implementar un cifrador en C proporciona:

- Control de bajo nivel (gestión directa de memoria y operaciones)
- Rendimiento optimizado
- Comprensión profunda de los algoritmos subyacentes

---

## Implementación Básica en C

### Estructura Principal

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <openssl/evp.h>
#include <openssl/rand.h>
#include <openssl/aes.h>

#define AES_KEY_SIZE 32
#define AES_BLOCK_SIZE 16

typedef struct {
    unsigned char key[AES_KEY_SIZE];
    unsigned char iv[AES_BLOCK_SIZE];
} crypto_context_t;

void generate_key(crypto_context_t *ctx) {
    if (RAND_bytes(ctx->key, AES_KEY_SIZE) != 1) exit(1);
    if (RAND_bytes(ctx->iv, AES_BLOCK_SIZE) != 1) exit(1);
}
```

---

### Función de Cifrado

```c
int encrypt_file(const char *input_file, const char *output_file, crypto_context_t *ctx) {
    FILE *in = fopen(input_file, "rb");
    FILE *out = fopen(output_file, "wb");
    EVP_CIPHER_CTX *cipher_ctx = EVP_CIPHER_CTX_new();
    EVP_EncryptInit_ex(cipher_ctx, EVP_aes_256_cbc(), NULL, ctx->key, ctx->iv);
    fwrite(ctx->iv, 1, AES_BLOCK_SIZE, out);

    unsigned char buffer[1024], encrypted[1024 + AES_BLOCK_SIZE];
    int bytes_read, encrypted_len;
    while ((bytes_read = fread(buffer, 1, sizeof(buffer), in)) > 0) {
        EVP_EncryptUpdate(cipher_ctx, encrypted, &encrypted_len, buffer, bytes_read);
        fwrite(encrypted, 1, encrypted_len, out);
    }
    EVP_EncryptFinal_ex(cipher_ctx, encrypted, &encrypted_len);
    fwrite(encrypted, 1, encrypted_len, out);

    EVP_CIPHER_CTX_free(cipher_ctx);
    fclose(in); fclose(out);
    return 0;
}
```

---

### Función de Descifrado

```c
int decrypt_file(const char *input_file, const char *output_file, crypto_context_t *ctx) {
    FILE *in = fopen(input_file, "rb");
    FILE *out = fopen(output_file, "wb");
    unsigned char iv[AES_BLOCK_SIZE];
    fread(iv, 1, AES_BLOCK_SIZE, in);

    EVP_CIPHER_CTX *cipher_ctx = EVP_CIPHER_CTX_new();
    EVP_DecryptInit_ex(cipher_ctx, EVP_aes_256_cbc(), NULL, ctx->key, iv);

    unsigned char buffer[1024], decrypted[1024 + AES_BLOCK_SIZE];
    int bytes_read, decrypted_len;
    while ((bytes_read = fread(buffer, 1, sizeof(buffer), in)) > 0) {
        EVP_DecryptUpdate(cipher_ctx, decrypted, &decrypted_len, buffer, bytes_read);
        fwrite(decrypted, 1, decrypted_len, out);
    }
    EVP_DecryptFinal_ex(cipher_ctx, decrypted, &decrypted_len);
    fwrite(decrypted, 1, decrypted_len, out);

    EVP_CIPHER_CTX_free(cipher_ctx);
    fclose(in); fclose(out);
    return 0;
}
```

---

### Gestión de Claves

```c
void derive_key_from_password(const char *password, const unsigned char *salt, crypto_context_t *ctx) {
    PKCS5_PBKDF2_HMAC(password, strlen(password), salt, 16, 10000, EVP_sha256(), AES_KEY_SIZE, ctx->key);
}

void save_key_to_file(const char *filename, crypto_context_t *ctx) {
    FILE *keyfile = fopen(filename, "wb");
    fwrite(ctx->key, 1, AES_KEY_SIZE, keyfile);
    fclose(keyfile);
}
```

---
