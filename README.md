# Ex-5 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
## Developed By : VIMALRAJ B
## Register Number : 212224230304

```

#include <stdio.h>
#include <string.h>

// Function to encrypt text using Rail Fence Cipher
void encryptRailFence(char* plaintext, int key, char* ciphertext) {
    int len = strlen(plaintext);
    int row, col = 0;
    int directionDown = 0; // Flag for direction
    char rail[key][len];

    // Initialize the rail matrix with '\n'
    for (row = 0; row < key; row++)
        for (col = 0; col < len; col++)
            rail[row][col] = '\n';

    row = 0; col = 0;

    // Fill the rail matrix in zig-zag manner
    for (int i = 0; i < len; i++) {
        rail[row][col++] = plaintext[i];

        if (row == 0 || row == key - 1)
            directionDown = !directionDown; // Change direction

        row += directionDown ? 1 : -1;
    }

    // Read the matrix row-wise to get ciphertext
    int index = 0;
    for (row = 0; row < key; row++)
        for (col = 0; col < len; col++)
            if (rail[row][col] != '\n')
                ciphertext[index++] = rail[row][col];

    ciphertext[index] = '\0';
}

// Function to decrypt text using Rail Fence Cipher
void decryptRailFence(char* ciphertext, int key, char* plaintext) {
    int len = strlen(ciphertext);
    char rail[key][len];
    int row, col;

    // Initialize the rail matrix with '\n'
    for (row = 0; row < key; row++)
        for (col = 0; col < len; col++)
            rail[row][col] = '\n';

    // Mark the places with '*'
    int directionDown = 0;
    row = 0; col = 0;
    for (int i = 0; i < len; i++) {
        rail[row][col++] = '*';
        if (row == 0 || row == key - 1)
            directionDown = !directionDown;
        row += directionDown ? 1 : -1;
    }

    // Fill the ciphertext characters in marked positions
    int index = 0;
    for (row = 0; row < key; row++)
        for (col = 0; col < len; col++)
            if (rail[row][col] == '*' && index < len)
                rail[row][col] = ciphertext[index++];

    // Read the matrix in zig-zag manner to reconstruct plaintext
    row = 0; col = 0;
    directionDown = 0;
    for (int i = 0; i < len; i++) {
        plaintext[i] = rail[row][col++];
        if (row == 0 || row == key - 1)
            directionDown = !directionDown;
        row += directionDown ? 1 : -1;
    }
    plaintext[len] = '\0';
}

int main() {
    char plaintext[1000], ciphertext[1000], decryptedText[1000];
    int key;

    printf("Enter plaintext: ");
    fgets(plaintext, sizeof(plaintext), stdin);
    plaintext[strcspn(plaintext, "\n")] = 0;

    printf("Enter Depth: ");
    scanf("%d", &key);

    encryptRailFence(plaintext, key, ciphertext);
    printf("Encrypted text: %s\n", ciphertext);

    decryptRailFence(ciphertext, key, decryptedText);
    printf("Decrypted text: %s\n", decryptedText);

    return 0;
}
```
# OUTPUT

<img width="452" height="314" alt="image" src="https://github.com/user-attachments/assets/1c01294d-adce-435e-981c-ccbcd03fb737" />


# RESULT

Thus,the program is executed successfully
