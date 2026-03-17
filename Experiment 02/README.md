# Experiment 2:

## Question:

- **Write a program that uses functions to perform the following operations on doubly linked list: I. Creation II. Insertion III. Deletion  IV. Traversal**
## Program:

```c
#include <stdio.h>
#include <stdlib.h>

// Define the doubly linked list structure
struct node {
    struct node *prev;
    int data;
    struct node *next;
};

// Function to create a new node
struct node* createNode(int data) {
    struct node *newNode = (struct node*)malloc(sizeof(struct node));
    newNode->prev = NULL;
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}

// Function to display the doubly linked list
void display(struct node *head) {
    if (head == NULL) {
        printf("Linked list is empty\n");
        return;
    }
    struct node *ptr = head;
    while (ptr != NULL) {
        printf("%d <-> ", ptr->data);
        ptr = ptr->next;
    }
    printf("NULL\n");
}

// Function to count the number of nodes in the doubly linked list
void count(struct node *head) {
    int count = 0;
    struct node *ptr = head;
    while (ptr != NULL) {
        count++;
        ptr = ptr->next;
    }
    printf("Number of nodes: %d\n", count);
}

// Function to insert at the beginning
struct node* insertAtBeginning(struct node *head, int data) {
    struct node *newNode = createNode(data);
    if (head != NULL) {
        newNode->next = head;
        head->prev = newNode;
    }
    return newNode;
}

// Function to insert at the end
struct node* insertAtEnd(struct node *head, int data) {
    struct node *newNode = createNode(data);
    if (head == NULL) return newNode;

    struct node *temp = head;
    while (temp->next != NULL) {
        temp = temp->next;
    }
    temp->next = newNode;
    newNode->prev = temp;
    return head;
}

// Function to insert at a specific position
struct node* insertAtPosition(struct node *head, int data, int position) {
    if (position == 1) {
        return insertAtBeginning(head, data);
    }

    struct node *newNode = createNode(data);
    struct node *temp = head;
    
    for (int i = 1; temp != NULL && i < position - 1; i++) {
        temp = temp->next;
    }

    if (temp == NULL) {
        printf("Position out of range.\n");
        return head;
    }

    newNode->next = temp->next;
    newNode->prev = temp;
    
    if (temp->next != NULL) {
        temp->next->prev = newNode;
    }
    temp->next = newNode;

    return head;
}

// Function to delete from the beginning
struct node* deleteFromBeginning(struct node *head) {
    if (head == NULL) {
        printf("List is empty.\n");
        return NULL;
    }
    struct node *temp = head;
    head = head->next;
    if (head != NULL) {
        head->prev = NULL;
    }
    free(temp);
    return head;
}

// Function to delete from the end
struct node* deleteFromEnd(struct node *head) {
    if (head == NULL) {
        printf("List is empty.\n");
        return NULL;
    }
    if (head->next == NULL) {
        free(head);
        return NULL;
    }

    struct node *temp = head;
    while (temp->next != NULL) {
        temp = temp->next;
    }

    temp->prev->next = NULL;
    free(temp);
    return head;
}

// Function to delete from a specific position
struct node* deleteFromPosition(struct node *head, int position) {
    if (head == NULL) {
        printf("List is empty.\n");
        return NULL;
    }

    struct node *temp = head;

    if (position == 1) {
        head = head->next;
        if (head != NULL) {
            head->prev = NULL;
        }
        free(temp);
        return head;
    }

    for (int i = 1; temp != NULL && i < position; i++) {
        temp = temp->next;
    }

    if (temp == NULL) {
        printf("Position out of range.\n");
        return head;
    }

    if (temp->next != NULL) {
        temp->next->prev = temp->prev;
    }
    if (temp->prev != NULL) {
        temp->prev->next = temp->next;
    }
    free(temp);
    return head;
}

int main() {
    struct node *head = NULL;
    int choice, data, position;

    while (1) {
        printf("\nMenu:\n");
        printf("1. Insert at Beginning\n");
        printf("2. Insert at End\n");
        printf("3. Insert at Position\n");
        printf("4. Delete from Beginning\n");
        printf("5. Delete from End\n");
        printf("6. Delete from Position\n");
        printf("7. Display List\n");
        printf("8. Count Nodes\n");
        printf("9. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter data: ");
                scanf("%d", &data);
                head = insertAtBeginning(head, data);
                break;

            case 2:
                printf("Enter data: ");
                scanf("%d", &data);
                head = insertAtEnd(head, data);
                break;

            case 3:
                printf("Enter data: ");
                scanf("%d", &data);
                printf("Enter position: ");
                scanf("%d", &position);
                head = insertAtPosition(head, data, position);
                break;

            case 4:
                head = deleteFromBeginning(head);
                printf("First node deleted.\n");
                break;

            case 5:
                head = deleteFromEnd(head);
                printf("Last node deleted.\n");
                break;

            case 6:
                printf("Enter position to delete: ");
                scanf("%d", &position);
                head = deleteFromPosition(head, position);
                printf("Node deleted from position %d.\n", position);
                break;

            case 7:
                printf("Linked List: ");
                display(head);
                break;

            case 8:
                count(head);
                break;

            case 9:
                printf("Exiting program.\n");
                return 0;

            default:
                printf("Invalid choice! Try again.\n");
        }
    }
    return 0;
}
```

## Output:
```c
Menu:
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete from Position
7. Display List
8. Count Nodes
9. Exit
Enter your choice: 1
Enter data: 455

Menu:
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete from Position
7. Display List
8. Count Nodes
9. Exit
Enter your choice: 1
Enter data: 666

Menu:
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete from Position
7. Display List
8. Count Nodes
9. Exit
Enter your choice: 2
Enter data: 888

Menu:
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete from Position
7. Display List
8. Count Nodes
9. Exit
Enter your choice: 3
Enter data: 999
Enter position: 2

Menu:
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete from Position
7. Display List
8. Count Nodes
9. Exit
Enter your choice: 7
Linked List: 666 <-> 999 <-> 455 <-> 888 <-> NULL

Menu:
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete from Position
7. Display List
8. Count Nodes
9. Exit
Enter your choice: 8
Number of nodes: 4

Menu:
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete from Position
7. Display List
8. Count Nodes
9. Exit
Enter your choice: 4
First node deleted.

Menu:
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete from Position
7. Display List
8. Count Nodes
9. Exit
Enter your choice: 5
Last node deleted.

Menu:
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete from Position
7. Display List
8. Count Nodes
9. Exit
Enter your choice: 7
Linked List: 999 <-> 455 <-> NULL

Menu:
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete from Position
7. Display List
8. Count Nodes
9. Exit
Enter your choice: 6
Enter position to delete: 2
Node deleted from position 2.

Menu:
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete from Position
7. Display List
8. Count Nodes
9. Exit
Enter your choice: 7
Linked List: 999 <-> NULL

Menu:
1. Insert at Beginning
2. Insert at End
3. Insert at Position
4. Delete from Beginning
5. Delete from End
6. Delete from Position
7. Display List
8. Count Nodes
9. Exit
Enter your choice: 9
Exiting program.
```