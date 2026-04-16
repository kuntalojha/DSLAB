# Experiment 6:

## Question:

- **Write a program that implements the following sorting methods to sort a given list of integers in ascending order. I. Radix Sort. II. Heap sort. III. Shell Sort. IV. Tree Short.**


## I. Radix Sort:
## Program:

```c
#include <stdio.h>

int getMax(int arr[], int n)
{
    int max = arr[0];
    for (int i = 1; i < n; i++)
        if (arr[i] > max)
            max = arr[i];
    return max;
}

void countSort(int arr[], int n, int exp)
{
    int output[100], count[10] = {0};

    for (int i = 0; i < n; i++)
        count[(arr[i] / exp) % 10]++;

    for (int i = 1; i < 10; i++)
        count[i] += count[i - 1];

    for (int i = n - 1; i >= 0; i--)
    {
        output[count[(arr[i] / exp) % 10] - 1] = arr[i];
        count[(arr[i] / exp) % 10]--;
    }

    for (int i = 0; i < n; i++)
        arr[i] = output[i];
}

void radixSort(int arr[], int n)
{
    for (int exp = 1; getMax(arr, n) / exp > 0; exp *= 10)
        countSort(arr, n, exp);
}

int main()
{
    int n, arr[100];

    printf("Radix Sort Implementation\n");
    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter elements for sorting: ");
    for (int i = 0; i < n; i++)
        scanf("%d", &arr[i]);

    radixSort(arr, n);

    printf("Sorted elements using Radix Sort: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
}
```

## Output:
```

```

## II. Heap sort:
## Program:

```c
#include <stdio.h>

void heapify(int arr[], int n, int i)
{
  int largest = i, l = 2 * i + 1, r = 2 * i + 2, t;

  if (l < n && arr[l] > arr[largest])
    largest = l;
  if (r < n && arr[r] > arr[largest])
    largest = r;

  if (largest != i)
  {
    t = arr[i];
    arr[i] = arr[largest];
    arr[largest] = t;
    heapify(arr, n, largest);
  }
}

void heapSort(int arr[], int n)
{
  for (int i = n / 2 - 1; i >= 0; i--)
    heapify(arr, n, i);
  for (int i = n - 1; i > 0; i--)
  {
    int t = arr[0];
    arr[0] = arr[i];
    arr[i] = t;
    heapify(arr, i, 0);
  }
}

int main()
{
  int n, arr[100];

  printf("Heap Sort Implementation\n");
  printf("Enter number of elements: ");
  scanf("%d", &n);

  printf("Enter elements for sorting: ");
  for (int i = 0; i < n; i++)
    scanf("%d", &arr[i]);

  heapSort(arr, n);

  printf("Sorted elements using Heap Sort: ");
  for (int i = 0; i < n; i++)
    printf("%d ", arr[i]);
}
```

## Output:
```

```

## III. Shell Sort:
## Program:

```c
#include <stdio.h>

void shellSort(int arr[], int n)
{
  for (int gap = n / 2; gap > 0; gap /= 2)
    for (int i = gap; i < n; i++)
    {
      int temp = arr[i], j;
      for (j = i; j >= gap && arr[j - gap] > temp; j -= gap)
        arr[j] = arr[j - gap];
      arr[j] = temp;
    }
}

int main()
{
  int n, arr[100];

  printf("Shell Sort Implementation\n");
  printf("Enter number of elements: ");
  scanf("%d", &n);

  printf("Enter elements for sorting: ");
  for (int i = 0; i < n; i++)
    scanf("%d", &arr[i]);

  shellSort(arr, n);

  printf("Sorted elements using Shell Sort: ");
  for (int i = 0; i < n; i++)
    printf("%d ", arr[i]);
}
```

## Output:
```

```

## IV. Tree Short:
## Program:

```c
#include <stdio.h>
#include <stdlib.h>

struct Node
{
  int data;
  struct Node *left, *right;
};

struct Node *insert(struct Node *root, int val)
{
  if (!root)
  {
    root = (struct Node *)malloc(sizeof(struct Node));
    root->data = val;
    root->left = root->right = NULL;
    return root;
  }
  if (val < root->data)
    root->left = insert(root->left, val);
  else
    root->right = insert(root->right, val);
  return root;
}

void inorder(struct Node *root)
{
  if (root)
  {
    inorder(root->left);
    printf("%d ", root->data);
    inorder(root->right);
  }
}

int main()
{
  int n, x;
  struct Node *root = NULL;

  printf("Tree Sort Implementation\n");
  printf("Enter number of elements: ");
  scanf("%d", &n);

  printf("Enter elements for sorting: ");
  for (int i = 0; i < n; i++)
  {
    scanf("%d", &x);
    root = insert(root, x);
  }

  printf("Sorted elements using Tree Sort:");
  inorder(root);
}
```

## Output:
```

```