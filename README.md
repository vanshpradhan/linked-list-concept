# linked-list-concept


#include <stdio.h>
#include <stdlib.h>

// Node structure
struct Node {
    int data;
    struct Node* next;
};

// Function to push a node at the beginning
void push(struct Node** head_ref, int new_data) {
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = *head_ref;
    *head_ref = new_node;
}

// Function to insert a new node in the middle
void insert_middle(struct Node* head, int new_data) {
    if (head == NULL) {
        return;
    }

    struct Node *slow = head, *fast = head;

    // Finding the middle node
    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }

    // Creating the new node to be inserted
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = new_data;

    // Insert the new node after the middle node
    new_node->next = slow->next;
    slow->next = new_node;
}

// Function to delete the middle node
void delete_middle(struct Node** head_ref) {
    if (*head_ref == NULL) {
        return;
    }

    if ((*head_ref)->next == NULL) {
        free(*head_ref);
        *head_ref = NULL;
        return;
    }

    struct Node *slow = *head_ref, *fast = *head_ref, *prev = NULL;

    // Finding the middle node
    while (fast != NULL && fast->next != NULL) {
        prev = slow;
        slow = slow->next;
        fast = fast->next->next;
    }

    // Delete the middle node
    if (prev != NULL) {
        prev->next = slow->next;
        free(slow);
    }
}

// Function to print the linked list
void print_list(struct Node* node) {
    while (node != NULL) {
        printf("%d -> ", node->data);
        node = node->next;
    }
    printf("NULL\n");
}

// Main function to demonstrate insert and delete operations
int main() {
    struct Node* head = NULL;

    // Creating the linked list
    push(&head, 5);
    push(&head, 4);
    push(&head, 3);
    push(&head, 2);
    push(&head, 1);

    printf("Original List:\n");
    print_list(head);

    // Insert a new node in the middle
    insert_middle(head, 100);
    printf("After Insertion:\n");
    print_list(head);

    // Delete the middle node
    delete_middle(&head);
    printf("After Deletion:\n");
    print_list(head);

    return 0;
}
