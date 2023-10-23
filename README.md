#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Contact {
    char name[50];
    char num[11];
    struct Contact* next;
} Contact;

Contact* start = NULL;

void Insert() {
    Contact* temp = (Contact*)malloc(sizeof(Contact));
    printf("\nContact name: ");
    scanf("%s", temp->name);
    printf("Mobile Number: ");
    scanf("%s", temp->num);
    temp->next = start;
    start = temp;
    printf("Record added\n");
}

void Delete() {
    char ch[50];
    printf("\nContact name: ");
    scanf("%s", ch);

    Contact* p = start;
    Contact* prev = NULL;

    while (p != NULL) {
        if (strcmp(p->name, ch) == 0) {
            if (prev == NULL) {
                start = p->next;
            } else {
                prev->next = p->next;
            }
            free(p);
            printf("Record deleted\n");
            return;
        }
        prev = p;
        p = p->next;
    }

    printf("Invalid Contact\n");
}

void Search() {
    char ch[50];
    printf("\nContact name: ");
    scanf("%s", ch);

    Contact* p = start;

    while (p != NULL) {
        if (strcmp(p->name, ch) == 0) {
            printf("\n%s\n%s\n", p->name, p->num);
            return;
        }
        p = p->next;
    }

    printf("Contact not found\n");
}

void Display() {
    Contact* p = start;
    int i = 1;

    while (p != NULL) {
        printf("\n%d. %s\nNumber: %s\n", i, p->name, p->num);
        p = p->next;
        i++;
    }

    if (i == 1) {
        printf("\nNo contacts in the phonebook\n");
    }
}

int main() {
    int choice;

    while (choice != 6) {
        printf("\n****************--------MINI PROJECT-PHONEBOOK MANAGEMENT SYSTEM--------****************\n");
        printf("1. Enter a new contact\n2. Delete a contact by name\n3. Search for a contact\n4. Display all contacts\n5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                Insert();
                break;
            case 2:
                Delete();
                break;
            case 3:
                Search();
                break;
            case 4:
                Display();
                break;
            case 5:
                exit(0);
            default:
                printf("Invalid choice\n");
        }
    }

    return 0;
}
