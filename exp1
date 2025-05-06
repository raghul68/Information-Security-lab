#include <stdio.h> 
#include <stdlib.h> 

int encrypt() { 
    char str[100]; 
    printf("\t\tInput String: "); 
    scanf("%s", str); 
    printf("\n\t\tEncrypted String: "); 
    for (int i = 0; str[i] != '\0'; i++) 
        printf("%c", str[i] + 3); 
} 

int decrypt() { 
    char str[100]; 
    printf("\t\tInput String: "); 
    scanf("%s", str); 
    printf("\n\t\tDecrypted String: "); 
    for (int i = 0; str[i] != '\0'; i++) 
        printf("%c", str[i] - 3); 
} 

int main() { 
    int choice; 
    char ch; 
    printf("\t\tConfidentiality\n"); 
    do { 
        printf("\t\tChoose operation\n\t\t1. Encryption\n\t\t2. Decryption\n\t\t3. Exit\n\t\t\n\t\t"); 
        scanf("%d", &choice); 
        switch (choice) { 
            case 1: 
                encrypt(); 
                break; 
            case 2: 
                decrypt(); 
                break; 
            case 3: 
                exit(0); 
                break; 
            default: 
                break; 
        } 
        printf("\n\t\tDo you want to continue (Y/N): "); 
        scanf(" %c", &ch); 
    } while (ch == 'y' || ch == 'Y'); 

    return 0; 
}
