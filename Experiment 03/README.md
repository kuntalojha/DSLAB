# Experiment 3:

## Question:

- **Write a program that uses functions to perform the following operations on circular linked list: I. Creation  II. Insertion  III. Deletion IV. Traversal**


## Program:

```c
#include <stdio.h>
#include <stdlib.h>

// Define structure
struct node
{
  int data;
  struct node *link;
};

// Create a new node
struct node *createNode(int data)
{
  struct node *newNode = (struct node *)malloc(sizeof(struct node));
  newNode->data = data;
  newNode->link = NULL;
  return newNode;
}

// Display list
void display(struct node *head)
{
  if (head == NULL)
  {
    printf("Linked list is empty\n");
    return;
  }

  struct node *ptr = head;

  do
  {
    printf("%d -> ", ptr->data);
    ptr = ptr->link;
  } while (ptr != head);

  printf("(head)\n");
}

// Count nodes
void count(struct node *head)
{
  if (head == NULL)
  {
    printf("Linked list is empty\n");
    return;
  }

  int count = 0;
  struct node *ptr = head;

  do
  {
    count++;
    ptr = ptr->link;
  } while (ptr != head);

  printf("Number of nodes: %d\n", count);
}

// Insert at beginning
struct node *insertAtBeginning(struct node *head, int data)
{
  struct node *newNode = createNode(data);

  if (head == NULL)
  {
    newNode->link = newNode;
    return newNode;
  }

  struct node *temp = head;

  while (temp->link != head)
  {
    temp = temp->link;
  }

  newNode->link = head;
  temp->link = newNode;
  head = newNode;

  return head;
}

// Insert at end
struct node *insertAtEnd(struct node *head, int data)
{
  struct node *newNode = createNode(data);

  if (head == NULL)
  {
    newNode->link = newNode;
    return newNode;
  }

  struct node *temp = head;

  while (temp->link != head)
  {
    temp = temp->link;
  }

  temp->link = newNode;
  newNode->link = head;

  return head;
}

// Insert at position
struct node *insertAtPosition(struct node *head, int data, int position)
{
  if (position == 1)
  {
    return insertAtBeginning(head, data);
  }

  struct node *newNode = createNode(data);
  struct node *temp = head;

  for (int i = 1; i < position - 1 && temp->link != head; i++)
  {
    temp = temp->link;
  }

  newNode->link = temp->link;
  temp->link = newNode;

  return head;
}

// Delete from beginning
struct node *deleteFromBeginning(struct node *head)
{
  if (head == NULL)
  {
    printf("List is empty\n");
    return NULL;
  }

  if (head->link == head)
  {
    free(head);
    return NULL;
  }

  struct node *temp = head;
  struct node *last = head;

  while (last->link != head)
  {
    last = last->link;
  }

  head = head->link;
  last->link = head;

  free(temp);

  printf("First node deleted\n");

  return head;
}

// Delete from end
struct node *deleteFromEnd(struct node *head)
{
  if (head == NULL)
  {
    printf("List is empty\n");
    return NULL;
  }

  if (head->link == head)
  {
    free(head);
    return NULL;
  }

  struct node *temp = head;
  struct node *prev = NULL;

  while (temp->link != head)
  {
    prev = temp;
    temp = temp->link;
  }

  prev->link = head;

  free(temp);

  printf("Last node deleted\n");

  return head;
}

// Delete from position
struct node *deleteFromPosition(struct node *head, int position)
{
  if (head == NULL)
  {
    printf("List is empty\n");
    return NULL;
  }

  if (position == 1)
  {
    return deleteFromBeginning(head);
  }

  struct node *temp = head;
  struct node *prev = NULL;

  for (int i = 1; i < position && temp->link != head; i++)
  {
    prev = temp;
    temp = temp->link;
  }

  prev->link = temp->link;
  free(temp);

  printf("Node deleted from position %d\n", position);

  return head;
}

int main()
{
  struct node *head = NULL;
  int choice, data, position;

  while (1)
  {
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

    switch (choice)
    {
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
      break;

    case 5:
      head = deleteFromEnd(head);
      break;

    case 6:
      printf("Enter position: ");
      scanf("%d", &position);
      head = deleteFromPosition(head, position);
      break;

    case 7:
      display(head);
      break;

    case 8:
      count(head);
      break;

    case 9:
      printf("Exiting...\n");
      return 0;

    default:
      printf("Invalid choice\n");
    }
  }
}
```

## Output:

```

```
































```
