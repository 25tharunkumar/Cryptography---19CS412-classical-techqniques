# Cryptography---19CS412-classical-techqniques


# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To develop a simple C program to implement Caeser Cipher.

## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
~~~
#include<stdio.h>
#include <string.h>
#include<conio.h>
#include <ctype.h>
int main()
{
char plain[10], cipher[10];
int key,i,length;
int result;
printf("\n Enter the plain text:");
scanf("%s", plain);
printf("\n Enter the key value:");
scanf("%d", &key);
printf("\n \n \t PLAIN TEXt: %s",plain);
printf("\n \n \t ENCRYPTED TEXT: ");
for(i = 0, length = strlen(plain); i < length; i++)
{
cipher[i]=plain[i] + key;
if (isupper(plain[i]) && (cipher[i] > 'Z'))
cipher[i] = cipher[i] - 26;
if (islower(plain[i]) && (cipher[i] > 'z'))
cipher[i] = cipher[i] - 26;
printf("%c", cipher[i]);
}
printf("\n \n \t AFTER DECRYPTION : ");
for(i=0;i<length;i++)
{
plain[i]=cipher[i]-key;
if(isupper(cipher[i])&&(plain[i]<'A'))
plain[i]=plain[i]+26;
if(islower(cipher[i])&&(plain[i]<'a'))
plain[i]=plain[i]+26;
printf("%c",plain[i]);
}
return 0;
}
~~~
## OUTPUT:
![Screenshot 2024-09-04 135833](https://github.com/user-attachments/assets/5a41f34a-765d-495b-81d4-d70d56747922)

## RESULT:
The program is executed successfully

---------------------------------


# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To develop a simple C program to implement PlayFair Cipher.

## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:

~~~
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define MX 5

void playfair(char ch1, char ch2, char key[MX][MX]) {
    int i, j, w, x, y, z;
    FILE *out;

    if ((out = fopen("cipher.txt", "a+")) == NULL) {
        printf("File Corrupted.\n");
        return;
    }

    // Initialize variables
    w = x = y = z = -1;

    for (i = 0; i < MX; i++) {
        for (j = 0; j < MX; j++) {
            if (ch1 == key[i][j]) {
                w = i;
                x = j;
            } else if (ch2 == key[i][j]) {
                y = i;
                z = j;
            }
        }
    }

    if (w == -1 || x == -1 || y == -1 || z == -1) {
        printf("Characters not found in key matrix.\n");
        fclose(out);
        return;
    }

    if (w == y) {
        x = (x + 1) % MX;
        z = (z + 1) % MX;
    } else if (x == z) {
        w = (w + 1) % MX;
        y = (y + 1) % MX;
    } else {
        int temp = x;
        x = z;
        z = temp;
    }

    printf("%c%c", key[w][x], key[y][z]);
    fprintf(out, "%c%c", key[w][x], key[y][z]);
    fclose(out);
}

int main() {
    int i, j, k = 0, l, m = 0, n;
    char key[MX][MX], keyminus[26] = {0}, keystr[10], str[25] = {0};
    char alpa[26] = {'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'};

    printf("\nEnter key: ");
    fgets(keystr, sizeof(keystr), stdin);
    keystr[strcspn(keystr, "\n")] = 0; // Remove newline character

    printf("\nEnter the plain text: ");
    fgets(str, sizeof(str), stdin);
    str[strcspn(str, "\n")] = 0; // Remove newline character

    n = strlen(keystr);

    // Convert characters to uppercase and replace 'J' with 'I'
    for (i = 0; i < n; i++) {
        if (keystr[i] == 'j') keystr[i] = 'i';
        keystr[i] = toupper(keystr[i]);
    }

    for (i = 0; i < strlen(str); i++) {
        if (str[i] == 'j') str[i] = 'i';
        str[i] = toupper(str[i]);
    }

    // Create keyminus array with remaining letters
    j = 0;
    for (i = 0; i < 26; i++) {
        for (k = 0; k < n; k++) {
            if (keystr[k] == alpa[i]) break;
            else if (alpa[i] == 'J') break;
        }
        if (k == n) keyminus[j++] = alpa[i];
    }

    // Construct key matrix
    k = 0;
    for (i = 0; i < MX; i++) {
        for (j = 0; j < MX; j++) {
            if (k < n) {
                key[i][j] = keystr[k++];
            } else {
                key[i][j] = keyminus[m++];
            }
            printf("%c ", key[i][j]);
        }
        printf("\n");
    }

    printf("\n\nEntered text: %s\nCipher Text: ", str);
    for (i = 0; i < strlen(str); i++) {
        if (str[i] == 'J') str[i] = 'I';
        if (str[i + 1] == '\0') {
            playfair(str[i], 'X', key);
        } else {
            if (str[i + 1] == 'J') str[i + 1] = 'I';
            if (str[i] == str[i + 1]) {
                playfair(str[i], 'X', key);
            } else {
                playfair(str[i], str[i + 1], key);
                i++;
            }
        }
    }
    return 0;
}
~~~
## OUTPUT:
![Screenshot 2024-09-04 140219](https://github.com/user-attachments/assets/f388f738-859e-436f-831c-f18f4de485f4)

## RESULT:
The program is executed successfully


---------------------------

# Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
~~~
#include <stdio.h>
#include <string.h>

#define MATRIX_SIZE 3

// Function to print matrix
void printMatrix(unsigned int matrix[MATRIX_SIZE][MATRIX_SIZE]) {
    for (int i = 0; i < MATRIX_SIZE; i++) {
        for (int j = 0; j < MATRIX_SIZE; j++) {
            printf("%d ", matrix[i][j]);
        }
        printf("\n");
    }
}

// Function to multiply matrix and vector
void multiplyMatrixVector(unsigned int matrix[MATRIX_SIZE][MATRIX_SIZE], unsigned int vector[MATRIX_SIZE], unsigned int result[MATRIX_SIZE]) {
    for (int i = 0; i < MATRIX_SIZE; i++) {
        unsigned int sum = 0;
        for (int j = 0; j < MATRIX_SIZE; j++) {
            sum += matrix[i][j] * vector[j];
        }
        result[i] = sum % 26;
    }
}

int main() {
    unsigned int a[MATRIX_SIZE][MATRIX_SIZE] = {{6, 24, 1}, {13, 16, 10}, {20, 17, 15}};
    unsigned int b[MATRIX_SIZE][MATRIX_SIZE] = {{8, 5, 10}, {21, 8, 21}, {21, 12, 8}};
    
    unsigned int c[MATRIX_SIZE], d[MATRIX_SIZE];
    char msg[20];
    
    printf("Enter plain text (up to 3 characters): ");
    scanf("%s", msg);
    
    // Ensure message length is 3 or less
    int msgLen = strlen(msg);
    if (msgLen > MATRIX_SIZE) {
        printf("Message too long. Limiting to %d characters.\n", MATRIX_SIZE);
        msgLen = MATRIX_SIZE;
    }
    
    // Convert message to numeric values
    for (int i = 0; i < msgLen; i++) {
        c[i] = msg[i] - 65;
        printf("%d ", c[i]);
    }
    printf("\n");
    
    // Encrypt
    multiplyMatrixVector(a, c, d);
    
    printf("Encrypted Cipher Text: ");
    for (int i = 0; i < MATRIX_SIZE; i++) {
        printf("%c ", d[i] + 65);
    }
    printf("\n");
    
    // Decrypt
    multiplyMatrixVector(b, d, c);
    
    printf("Decrypted Cipher Text: ");
    for (int i = 0; i < MATRIX_SIZE; i++) {
        printf("%c ", c[i] + 65);
    }
    printf("\n");
    
    return 0;
}

~~~
## OUTPUT:
![Screenshot 2024-09-04 140509](https://github.com/user-attachments/assets/db92d069-a4b8-4f34-ac06-27c3c59dea78)

## RESULT:
The program is executed successfully

-------------------------------------------------

# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
~~~
#include <stdio.h>
#include <ctype.h>
#include <string.h>
#include <stdlib.h>

void encipher();
void decipher();

int main() {
    int choice;
    while (1) {
        printf("\n1. Encrypt Text");
        printf("\n2. Decrypt Text");
        printf("\n3. Exit");
        printf("\n\nEnter Your Choice: ");
        scanf("%d", &choice);
        
        switch (choice) {
            case 1:
                encipher();
                break;
            case 2:
                decipher();
                break;
            case 3:
                exit(0);
            default:
                printf("Please Enter a Valid Option.");
        }
    }
}

void encipher() {
    unsigned int i, j;
    char input[50], key[10];
    
    // Clear input buffer
    while (getchar() != '\n');
    
    printf("\nEnter Plain Text: ");
    fgets(input, sizeof(input), stdin);
    input[strcspn(input, "\n")] = 0; // Remove newline character
    
    printf("\nEnter Key Value: ");
    fgets(key, sizeof(key), stdin);
    key[strcspn(key, "\n")] = 0; // Remove newline character
    
    printf("\nResultant Cipher Text: ");
    for (i = 0, j = 0; i < strlen(input); i++, j++) {
        if (j >= strlen(key)) {
            j = 0;
        }
        // Encrypt character
        printf("%c", 65 + (((toupper(input[i]) - 65) + (toupper(key[j]) - 65)) % 26));
    }
    printf("\n");
}

void decipher() {
    unsigned int i, j;
    char input[50], key[10];
    int value;
    
    // Clear input buffer
    while (getchar() != '\n');
    
    printf("\nEnter Cipher Text: ");
    fgets(input, sizeof(input), stdin);
    input[strcspn(input, "\n")] = 0; // Remove newline character
    
    printf("\nEnter Key Value: ");
    fgets(key, sizeof(key), stdin);
    key[strcspn(key, "\n")] = 0; // Remove newline character
    
    printf("\nResultant Plain Text: ");
    for (i = 0, j = 0; i < strlen(input); i++, j++) {
        if (j >= strlen(key)) {
            j = 0;
        }
        // Decrypt character
        value = (toupper(input[i]) - 65) - (toupper(key[j]) - 65);
        if (value < 0) {
            value += 26; // Ensure result is positive
        }
        printf("%c", 65 + (value % 26));
    }
    printf("\n");
}

~~~
## OUTPUT:
![Screenshot 2024-09-04 140704](https://github.com/user-attachments/assets/e59f83fa-8d0b-44a4-92cc-f8788a84f483)

## RESULT:
The program is executed successfully

-----------------------------------------------------------------------

# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
~~~
#include <stdio.h>
#include <string.h>

#define MAX_LENGTH 20

void railFenceEncryption(char *input, char *output) {
    int length = strlen(input);
    int i, j = 0;

    // Apply rail fence encryption
    for (i = 0; i < length; i++) {
        if (i % 2 == 0) {
            output[j++] = input[i];
        }
    }
    for (i = 0; i < length; i++) {
        if (i % 2 == 1) {
            output[j++] = input[i];
        }
    }
    output[j] = '\0';  // Null-terminate the string
}

void railFenceDecryption(char *cipherText, char *decryptedText) {
    int length = strlen(cipherText);
    int k, i, j = 0;

    // Calculate the split point
    if (length % 2 == 0) {
        k = length / 2;
    } else {
        k = (length / 2) + 1;
    }

    // Reconstruct the original string
    for (i = 0; i < k; i++) {
        decryptedText[j] = cipherText[i];
        j += 2;
    }
    j = 1;
    for (i = k; i < length; i++) {
        decryptedText[j] = cipherText[i];
        j += 2;
    }
    decryptedText[length] = '\0';  // Null-terminate the string
}

int main() {
    char input[MAX_LENGTH], cipherText[MAX_LENGTH], decryptedText[MAX_LENGTH];

    printf("\n\t\tRAIL FENCE TECHNIQUE");
    printf("\n\nEnter the input string (up to 19 characters): ");
    fgets(input, sizeof(input), stdin);
    input[strcspn(input, "\n")] = '\0';  // Remove newline character

    railFenceEncryption(input, cipherText);
    printf("\nCipher text after applying rail fence: %s\n", cipherText);

    railFenceDecryption(cipherText, decryptedText);
    printf("Text after decryption: %s\n", decryptedText);

    return 0;
}

~~~
## OUTPUT:
![Screenshot 2024-09-04 140937](https://github.com/user-attachments/assets/96023545-f45a-49e8-9d5b-500cb7b3c9da)


## RESULT:
The program is executed successfully
