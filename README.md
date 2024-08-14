# linked-list-concept


#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};


void push(struct Node** head_ref, int new_data) {
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = *head_ref;
    *head_ref = new_node;
}



void insert_middle(struct Node* head, int new_data) {
    if (head == NULL) {
        return;
    }

    struct Node *slow = head, *fast = head;

    
    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }


    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = new_data;

  
    new_node->next = slow->next;
    slow->next = new_node;
}


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

    
    while (fast != NULL && fast->next != NULL) {
        prev = slow;
        slow = slow->next;
        fast = fast->next->next;
    }

 
    if (prev != NULL) {
        prev->next = slow->next;
        free(slow);
    }
}


void print_list(struct Node* node) {
    while (node != NULL) {
        printf("%d -> ", node->data);
        node = node->next;
    }
    printf("NULL\n");
}


int main() {
    struct Node* head = NULL;

   
    push(&head, 5);
    push(&head, 4);
    push(&head, 3);
    push(&head, 2);
    push(&head, 1);

    printf("Original List:\n");
    print_list(head);

   
    insert_middle(head, 100);
    printf("After Insertion:\n");
    print_list(head);

   
    delete_middle(&head);
    printf("After Deletion:\n");
    print_list(head);

    return 0;
}
