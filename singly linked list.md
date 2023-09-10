#include <stdio.h>
#include <stdlib.h>
struct Node {
    int data;
    struct Node* next;
};
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    if (newNode == NULL) {
        printf("Memory allocation failed.\n");
        exit(1);
    }
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}
struct Node* insertAtBeginning(struct Node* head, int data) {
    struct Node* newNode = createNode(data);
    newNode->next = head;
    return newNode;
}
struct Node* insertAtEnd(struct Node* head, int data) {
    struct Node* newNode = createNode(data);
    if (head == NULL) {
        return newNode;
    }
    struct Node* current = head;
    while (current->next != NULL) {
        current = current->next;
    }
    current->next = newNode;
    return head;
}
struct Node* insertAtPosition(struct Node* head, int data, int position) {
    if (position <= 0) {
        printf("Invalid position.\n");
        return head;
    }
    if (position == 1) {
        return insertAtBeginning(head, data);
    }
    struct Node* newNode = createNode(data);
    struct Node* current = head;
    for (int i = 1; i < position - 1 && current != NULL; i++) {
        current = current->next;
    }
    if (current == NULL) {
        printf("Invalid position.\n");
        return head;
    }
    newNode->next = current->next;
    current->next = newNode;
    return head;
}
struct Node* deleteAtBeginning(struct Node* head) {
    if (head == NULL) {
        printf("List is empty.\n");
        return NULL;
    }
    struct Node* temp = head;
    head = head->next;
    free(temp);
    return head;
}
struct Node* deleteAtEnd(struct Node* head) {
    if (head == NULL) {
        printf("List is empty.\n");
        return NULL;
    }
    if (head->next == NULL) {
        free(head);
        return NULL;
    }
    struct Node* current = head;
    while (current->next->next != NULL) {
        current = current->next;
    }
    free(current->next);
    current->next = NULL;
    return head;
}
struct Node* deleteAtPosition(struct Node* head, int position) {
    if (head == NULL) {
        printf("List is empty.\n");
        return NULL;
    }
    if (position <= 0) {
        printf("Invalid position.\n");
        return head;
    }
    if (position == 1) {
        struct Node* temp = head;
        head = head->next;
        free(temp);
        return head;
    }
    struct Node* current = head;
    for (int i = 1; i < position - 1 && current != NULL; i++) {
        current = current->next;
    }
    if (current == NULL || current->next == NULL) {
        printf("Invalid position.\n");
        return head;
    }
    struct Node* temp = current->next;
    current->next = current->next->next;
    free(temp);
    return head;
}
int search(struct Node* head, int target) {
    struct Node* current = head;
    int position = 1;
    while (current != NULL) {
        if (current->data == target) {
            return position;
        }
        position++;
        current = current->next;
    }
    return -1;
}
int countNodes(struct Node* head) {
    struct Node* current = head;
    int count = 0;
    while (current != NULL) {
        count++;
        current = current->next;
    }
    return count;
}
void display(struct Node* head) {
    struct Node* current = head;
    while (current != NULL) {
        printf("%d ", current->data);
        current = current->next;
    }
    printf("\n");
}
int main() {
    struct Node* head = NULL;
    int choice, data, position;
    while (1) {
        printf("\nLinked List Operations:\n");
        printf("1. Insert at Beginning\n");
        printf("2. Insert at End\n");
        printf("3. Insert at Position\n");
        printf("4. Delete at Beginning\n");
        printf("5. Delete at End\n");
        printf("6. Delete at Position\n");
        printf("7. Search\n");
        printf("8. Count Nodes\n");
        printf("9. Display\n");
        printf("10. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        switch (choice) {
            case 1:
                printf("Enter data to insert: ");
                scanf("%d", &data);
                head = insertAtBeginning(head, data);
                break;
            case 2:
                printf("Enter data to insert: ");
                scanf("%d", &data);
                head = insertAtEnd(head, data);
                break;
            case 3:
                printf("Enter data to insert: ");
                scanf("%d", &data);
                printf("Enter position: ");
                scanf("%d", &position);
                head = insertAtPosition(head, data, position);
                break;
            case 4:
                head = deleteAtBeginning(head);
                break;
            case 5:
                head = deleteAtEnd(head);
                break;
            case 6:
                printf("Enter position: ");
                scanf("%d", &position);
                head = deleteAtPosition(head, position);
                break;
            case 7:
                printf("Enter data to search for: ");
                scanf("%d", &data);
                position = search(head, data);
                if (position != -1) {
                    printf("Data found at position %d\n", position);
                } else {
                    printf("Data not found.\n");
                }
                break;
            case 8:
                printf("Number of nodes: %d\n", countNodes(head));
                break;
            case 9:
                printf("Linked List: ");
                display(head);
                break;
            case 10:
                exit(0);
            default:
                printf("Invalid choice.\n");
        }
    }
    return 0;
}
