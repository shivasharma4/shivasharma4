#include <stdio.h>
#include <stdlib.h>
struct Node {
    int data;
    struct Node* next;
};
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    if (newNode == NULL) {
        printf("Memory allocation failed!\n");
        exit(1);
    }
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}
void addNode(struct Node** head, int data) {
    struct Node* newNode = createNode(data);
    if (*head == NULL) {
        *head = newNode;
        newNode->next = *head;
    } else {
        struct Node* temp = *head;
        while (temp->next != *head) {
            temp = temp->next;
        }
        temp->next = newNode;
        newNode->next = *head;
    }
}
void deleteNode(struct Node** head, int key) {
    if (*head == NULL) {
        printf("List is empty. Deletion not possible.\n");
        return;
    }
    struct Node* current = *head;
    struct Node* prev = NULL;
    while (current->data != key) {
        if (current->next == *head) {
            printf("Node with data %d not found.\n", key);
            return;
        }
        prev = current;
        current = current->next;
    }
    if (current->next == *head && prev == NULL) {
        *head = NULL;
        free(current);
        return;
    }
    if (current == *head) {
        struct Node* temp = *head;
        while (temp->next != *head) {
            temp = temp->next;
        }
        *head = current->next;
        temp->next = *head;
    } else {
        prev->next = current->next;
    }
    free(current);
}
void displayList(struct Node* head) {
    struct Node* current = head;
    if (head == NULL) {
        printf("List is empty.\n");
        return;
    }
    printf("Circular Linked List: ");
    do {
        printf("%d -> ", current->data);
        current = current->next;
    } while (current != head);
    printf("\n");
}
int main() {
    struct Node* head = NULL;
    addNode(&head, 5);
    addNode(&head, 10);
    addNode(&head, 7);
    displayList(head);
    deleteNode(&head, 10);
    deleteNode(&head, 5);
    displayList(head);
    return 0;
}

