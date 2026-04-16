# Experiment 7:

## Question:

- **Write a program to implement the tree traversal methods (Recursive and Non-Recursive).**

## Program:

```c
#include <stdio.h>
#include <stdlib.h>

struct Node
{
  int data;
  struct Node *left, *right;
};

//  create a new node
struct Node *create(int val)
{
  struct Node *n = (struct Node *)malloc(sizeof(struct Node));
  n->data = val;
  n->left = n->right = NULL;
  return n;
}

// insert a value into the BST
struct Node *insert(struct Node *root, int val)
{
  if (root == NULL)
    return create(val);
  if (val < root->data)
    root->left = insert(root->left, val);
  else
    root->right = insert(root->right, val);
  return root;
}

// Recursive Traversals
void inorderR(struct Node *root)
{
  if (root)
  {
    inorderR(root->left);
    printf("%d ", root->data);
    inorderR(root->right);
  }
}

void preorderR(struct Node *root)
{
  if (root)
  {
    printf("%d ", root->data);
    preorderR(root->left);
    preorderR(root->right);
  }
}

void postorderR(struct Node *root)
{
  if (root)
  {
    postorderR(root->left);
    postorderR(root->right);
    printf("%d ", root->data);
  }
}

// Non-Recursive Traversals using stack
struct Node *stack[100];
int top = -1;

void push(struct Node *n) { stack[++top] = n; }
struct Node *pop() { return stack[top--]; }
int isEmpty() { return top == -1; }

// Inorder (Non-Recursive)
void inorderNR(struct Node *root)
{
  struct Node *curr = root;
  while (curr || !isEmpty())
  {
    while (curr)
    {
      push(curr);
      curr = curr->left;
    }
    curr = pop();
    printf("%d ", curr->data);
    curr = curr->right;
  }
}

// Preorder (Non-Recursive)
void preorderNR(struct Node *root)
{
  if (!root)
    return;
  push(root);

  while (!isEmpty())
  {
    struct Node *curr = pop();
    printf("%d ", curr->data);

    if (curr->right)
      push(curr->right);
    if (curr->left)
      push(curr->left);
  }
}

// Postorder (Non-Recursive using 2 stacks logic simplified)
void postorderNR(struct Node *root)
{
  struct Node *s1[100], *s2[100];
  int t1 = -1, t2 = -1;

  if (root)
    s1[++t1] = root;

  while (t1 != -1)
  {
    struct Node *temp = s1[t1--];
    s2[++t2] = temp;

    if (temp->left)
      s1[++t1] = temp->left;
    if (temp->right)
      s1[++t1] = temp->right;
  }

  while (t2 != -1)
    printf("%d ", s2[t2--]->data);
}


int main()
{
  int n, x;
  struct Node *root = NULL;

  printf("Enter number of nodes: ");
  scanf("%d", &n);

  printf("Enter values: ");
  for (int i = 0; i < n; i++)
  {
    scanf("%d", &x);
    root = insert(root, x);
  }

  // Recursive
  printf("\nRecursive Inorder: ");
  inorderR(root);

  printf("\nRecursive Preorder: ");
  preorderR(root);

  printf("\nRecursive Postorder: ");
  postorderR(root);

  // Non-Recursive
  printf("\n\nNon-Recursive Inorder: ");
  inorderNR(root);

  printf("\nNon-Recursive Preorder: ");
  preorderNR(root);

  printf("\nNon-Recursive Postorder: ");
  postorderNR(root);

  return 0;
}
```

## Output:

```

```
