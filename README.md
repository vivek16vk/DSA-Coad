# DSA-Code
# Experiment No.1
# Write a program to find the largest number in an array of integer Analyze its time and space complexity...

Program:
#include <stdio.h>
#include <limits.h>
#include <time.h>
#include<conio.h>
int find_largest(int arr[], int n) {
if (n <= 0) {
printf("Array is empty\n");
return INT_MIN;
}
int largest = arr[0];
for (int i = 1; i < n; i++) {
if (arr[i] > largest) {
largest = arr[i];
}
}
return largest;
}
int main() {
int array[] = {3, 5, 7, 2, 8, -1, 4, 10, 12};
int n = sizeof(array) / sizeof(array[0]);
clock_t start, end;
double cpu_time_used;
start = clock();
int largest = find_largest(array, n);
end = clock();
cpu_time_used = ((double) (end - start)) / CLOCKS_PER_SEC;
if (largest != INT_MIN) {
printf("The largest number is: %d\n", largest);
}
printf("Execution time: %f seconds\n", cpu_time_used);
getch ();
}
Output : The largest number is: 12 Execution time: 0.000001 second

# Implement a stack data strcture using array and linked list....
# Exprement no : 2
#include <stdio.h>
#include <limits.h>
#define MAX 3typedef
#include<conio.h>
struct {
int items[MAX];
int top; } Stack;
void initStack(Stack* stack) {
stack->top = -1;
}
int isFull(Stack* stack) {
return stack->top == MAX - 1;
}
int isEmpty(Stack* stack) {
return stack->top == -1;
}
void push(Stack* stack, int item) {
if (isFull(stack)) {
printf("Stack overflow\n");
} else {
stack->top++;
stack->items[stack->top] = item;
printf("%d pushed to stack\n", item);
}
}
int pop(Stack* stack) {if
(isEmpty(stack)) {
printf("Stack underflow\n");
return INT_MIN;
} else {
int item = stack->items[stack->top];
stack->top--;
return item;
}
}
int peek(Stack* stack) {
if (isEmpty(stack)) {
printf("Stack is empty\n");
 return INT_MIN;
} else {
return stack->items[stack->top];
}
}
int main() {
Stack stack;
initStack(&stack);
push(&stack, 10);
push(&stack, 20);
push(&stack, 30);
push(&stack, 40); // This will cause stack overflow
printf("Top element is %d\n", peek(&stack));
pop(&stack);
pop(&stack);
pop(&stack);
pop(&stack); // This will cause stack underflow
getch();
}
Output
10 pushed to stack
20 pushed to stack
30 pushed to stack Stack
overflow Top element is
30
30 popped from stack
20 popped from stack
10 popped from stack Stack
underflow

# Implement a linear queue data structure using arrays and link list ...
# Experiment no : 3

# Linear queue
#include<stdio.h>
#include <stdlib.h>
#include<conio.h>
 #define MAX_SIZE 100
// Structure for the Queue typedef struct {
int items[MAX_SIZE];
int front; // Index of the front element
int rear; // Index of the rear element
} Queue;
// Function to initialize the queue void initQueue(Queue *q) {
q->front = -1; // Initialize front index
q->rear = -1; // Initialize rear index
}
// Function to check if the queue is empty
int isEmpty(Queue *q) {
return (q->front == -1 && q->rear == -1);
}
// Function to check if the queue is full
int isFull(Queue *q) {
return (q->rear == MAX_SIZE - 1);
}
// Function to add an element to the queue (enqueue operation)
void enqueue(Queue *q, int value) {
if (isFull(q)) {
printf("Queue is full. Cannot enqueue.\n");
return;
}
if (isEmpty(q)) {
q->front = 0; // Initialize front if it's the first element
}
q->rear++; // Move rear to the next position
q->items[q->rear] = value; // Add the new element to the rear
}
// Function to remove an element from the queue (dequeue operation)
int dequeue(Queue *q) {
int removedItem;
if (isEmpty(q)) {
printf("Queue is empty. Cannot dequeue.\n");
return -1;
}
removedItem = q->items[q->front]; // Get the element at the frontif
(q->front == q->rear) {
// Reset queue to empty state if there was only one element
q->front = -1;
q->rear = -1;
} else {
q->front++; // Move front to the next position
}
return removedItem;
}
// Function to retrieve the element at the front of the queue without removing it
int front(Queue *q) {
if (isEmpty(q)) {
printf("Queue is empty. No front element.\n");
return -1;
}
return q->items[q->front];
}
// Function to display the elements in the queue
void display(Queue *q) {
if (isEmpty(q)) {
printf("Queue is empty. Nothing to display.\n");
return;
}
printf("Queue elements: ");
for (int i = q->front; i <= q->rear; i++) {
printf("%d ", q->items[i]);
}
printf("\n");
}
int main() {
Queue q;
initQueue(&q);
enqueue(&q, 10);
enqueue(&q, 20);
enqueue(&q, 30);
display(&q); // Output: Queue elements: 10 20 30
printf("Front element: %d\n", front(&q)); // Output: Front element: 10
dequeue(&q); // Remove the front element
display(&q); // Output: Queue elements: 20 30
getch();
}

# Linked list
#include<stdio.h>
#include <stdlib.h>
#include<conio.h> 
// Define a structure for a 
Nodetypedef struct Node {
int data;
// Data stored in the node
struct Node *next; // Pointer to the next node
} Node;
// Define a structure for the Queue
typedef struct {
Node *front; // Pointer to the front (oldest) node
Node *rear; // Pointer to the rear (newest) node
} Queue;
// Function to initialize the queue
void initQueue(Queue *q) {
q->front = NULL;
q->rear = NULL;
}
// Function to check if the queue is empty
int isEmpty(Queue *q) {
return (q->front == NULL);
}
// Function to add an element to the queue (enqueue operation)
void enqueue(Queue *q, int value) {
// Create a new node
Node *newNode = (Node *)malloc(sizeof(Node));
if (newNode == NULL) {
printf("Memory allocation failed.\n");
return;
}
newNode->data = value;
newNode->next = NULL;
// If queue is empty, set both front and rear to the new nodeif
(isEmpty(q)) {
q->front = newNode;
q->rear = newNode;
} else {
// Add the new node at the end of the queue
q->rear->next = newNode;
q->rear = newNode;
}
}
 // Function to remove an element from the queue (dequeue operation)int dequeue(Queue *q) {
if (isEmpty(q)) {
printf("Queue is empty. Cannot dequeue.\n");
return -1;
}
// Retrieve data from the front node
Node *temp = q->front;
int removedItem = temp->data;
// Move front to the next node
q->front = q->front->next;
// Free memory of the dequeued node
free(temp);
// If front becomes NULL, set rear to NULL as well
if (q->front == NULL) {
q->rear = NULL;
}
return removedItem;
}
// Function to retrieve the element at the front of the queue without removing it
int front(Queue *q) {
if (isEmpty(q)) {
printf("Queue is empty. No front element.\n");
return -1;
}
return q->front->data;
}
// Function to display the elements in the queue
void display(Queue *q) {
if (isEmpty(q)) {
printf("Queue is empty. Nothing to display.\n");
return; }
printf("Queue elements: "); Node *current = q->front; while (current != NULL) {
printf("%d ", current->data);
current = current->next;
}
printf("\n");
}
// Function to free memory allocated for the queue nodes
void freeQueue(Queue *q) {
Node *current = q->front;
Node *next;
while (current != NULL) {
next = current->next;
free(current);
current = next;
}
q->front = NULL;
q->rear = NULL;
}
int main() {
Queue q;
initQueue(&q);
enqueue(&q, 10);
enqueue(&q, 20);
enqueue(&q, 30);
display(&q); // Output: Queue elements: 10 20 30
printf("Dequeued item: %d\n", dequeue(&q)); // Output: Dequeued item: 10display(&q);
// Output: Queue elements: 20 30
printf("Front item: %d\n", front(&q)); // Output: Front item: 20
freeQueue(&q); // Free memory allocated for the queue nodes
getch();
}

# Write a program to implement Circular Linked List. 
# Experiment no : 4

#include<stdio.h>
#include <stdlib.h>
#include<conio.h>
struct Node {
int data; struct Node* next;
};
void insertAtBeginning(struct Node** head, int data) {
struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
newNode->data = data;
if (*head == NULL) {
newNode->next = newNode;
*head = newNode;
} else {
struct Node* temp = *head;
while (temp->next != *head) {
temp = temp->next;
}
newNode->next = *head;
temp->next = newNode;
*head = newNode;
}
}
void insertAtEnd(struct Node** head, int data) {
struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
newNode->data = data;
if (*head == NULL) {
newNode->next = newNode;
*head = newNode;
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
return;
}
struct Node *temp = *head, *prev;
if (temp->data == key && temp->next == *head) {
*head = NULL;
free(temp);
return;
}
if (temp->data == key) {
while (temp->next != *head) {
temp = temp->next;
}
temp->next = (*head)->next;
free(*head);
*head = temp->next;
} else {
while (temp->next != *head && temp->data != key) {
prev = temp;
temp = temp->next;
}
if (temp->data == key) {
prev->next = temp->next;
free(temp);
}
}
}
void traverse(struct Node* head) {
if (head == NULL) {
return;
}
struct Node* temp = head;
do {
printf("%d ", temp->data);
temp = temp->next;
} while (temp != head);
printf("\n");
}
int main() {
struct Node* head = NULL;
insertAtBeginning(&head, 10);
insertAtBeginning(&head, 20);
insertAtBeginning(&head, 30);
printf("Circular Linked List after inserting at beginning:\n");
traverse(head);
insertAtEnd(&head, 40);
insertAtEnd(&head, 50);
printf("Circular Linked List after inserting at end:\n");
traverse(head);
deleteNode(&head, 20);
printf("Circular Linked List after deleting a node:\n");
traverse(head);
getch();
}
Output:
Circular Linked List after inserting at beginning:
30 20 10
Circular Linked List after inserting at end:
30 20 10 40 50
Circular Linked List after deleting a node:
30 10 40 50

# Write a program to search for an element in an array using linear search and binary search. Compare their efficiencies.
# Experiment no : 5

#include <stdio.h>
#include<conio.h>
// Function for linear search
int linearSearch(int arr[], int n, int key, int *comparisons) {
for (int i = 0; i < n; i++) {
(*comparisons)++;
if (arr[i] == key) {
return i; // Return index of key if found
}
}
return -1; // Return -1 if key not found
}
// Function for binary search (array must be sorted)
int binarySearch(int arr[], int left, int right, int key, int *comparisons) {while
(left <= right) {
(*comparisons)++;
int mid = left + (right - left) / 2;
// Check if key is present at mid
if (arr[mid] == key) {
return mid; // Return index of key if found
}
// If key is greater, ignore left half
if (arr[mid] < key) {
left = mid + 1;
}
// If key is smaller, ignore right half
else {
right = mid - 1;
}
}
return -1; // Return -1 if key not found
}
int main() {
int arr[] = {2, 5, 8, 12, 16, 23, 38, 56, 72, 91};
int n = sizeof(arr) / sizeof(arr[0]);
int key = 23;
// Perform linear search
int comparisons_linear = 0;
int result_linear = linearSearch(arr, n, key, &comparisons_linear);
// Perform binary search (array must be sorted)
int comparisons_binary = 0;
int result_binary = binarySearch(arr, 0, n - 1, key, &comparisons_binary);
// Print results
if (result_linear != -1) {
printf("Linear Search:\n");
printf("Element %d found at index %d\n", key, result_linear);
printf("Number of comparisons: %d\n", comparisons_linear);
} else {
printf("Linear Search:\n");
printf("Element %d not found\n", key);
printf("Number of comparisons: %d\n", comparisons_linear);
}
printf("\n");
if (result_binary != -1) {
printf("Binary Search:\n");
printf("Element %d found at index %d\n", key, result_binary);
printf("Number of comparisons: %d\n", comparisons_binary);
} else {
printf("Binary Search:\n");
printf("Element %d not found\n", key);
printf("Number of comparisons: %d\n", comparisons_binary);
}
getch();
}
Output
Linear Search:
Element 23 found at index 5 Number
of comparisons: 6
Binary Search:
Element 23 found at index 5 Number
of comparisons: 3

 # Write a program to sort the elements using
# 1) Bubble Sort
2) Insertion Sort
3) Selection Sort

#include <stdio.h>
#include<conio.h>
// Function to perform Bubble Sort
void bubbleSort(int arr[], int n) {
int i, j;
for (i = 0; i < n - 1; i++) {
// Last i elements are already in place
for (j = 0; j < n - i - 1; j++) {
// Swap if the element found is greater than the next element
if (arr[j] > arr[j + 1]) {
int temp = arr[j];
arr[j] = arr[j + 1];
arr[j + 1] = temp;
}
}
}
}
// Function to print the array
void printArray(int arr[], int size) {
for (int i = 0; i < size; i++) {
printf("%d ", arr[i]);
}
printf("\n");
}
int main() {
int arr[] = {64, 34, 25, 12, 22, 11, 90};
int n = sizeof(arr) / sizeof(arr[0]);
printf("Original array: \n");
printArray(arr, n);
// Perform Bubble Sort
bubbleSort(arr, n);
printf("Sorted array in ascending order: \n");
printArray(arr, n);
getch();
}

# 2) Inserstion Sort:

#include <stdio.h>
#include<conio.h>
// Function to perform Insertion Sort void
insertionSort(int arr[], int n) {
int i, j, key;
for (i = 1; i < n; i++{
key = arr[i];
j = i - 1;
// Move elements of arr[0..i-1], that are greater than key, to one position ahead of theircurrent
position
while (j >= 0 && arr[j] > key) {
arr[j + 1] = arr[j];
j = j - 1;
}
arr[j + 1] = key;
}
}
// Function to print the array void
printArray(int arr[], int size) { for 
(int i = 0; i < size; i++) {
printf("%d ", arr[i]);
}
printf("\n");
}
int main() {
int arr[] = {12, 11, 13, 5, 6};
int n = sizeof(arr) / sizeof(arr[0]);
printf("Original array: \n");
printArray(arr, n);
// Perform Insertion Sort
insertionSort(arr, n);
printf("Sorted array in ascending order: \n");
printArray(arr, n);
getch();
}

# 3) Selection Sort

#include <stdio.h>
#include<conio.h>
void selectionSort(int arr[], int n) 
{int i, j, min_index;
for (i = 0; i < n-1; i++) {
min_index = i;
for (j = i+1; j < n; j++) {
if (arr[j] < arr[min_index]) {
min_index = j;
}
}
// Swap the found minimum element with the first element
int temp = arr[min_index];
arr[min_index] = arr[i];
arr[i] = temp;
}
}
int main() {
int n, i;
printf("Enter number of elements: ");
scanf("%d", &n);
int arr[n];
printf("Enter elements:\n");
for (i = 0; i < n; i++) {
scanf("%d", &arr[i]);
}
selectionSort(arr, n);
printf("Sorted array:\n");
for (i = 0; i < n; i++) {
printf("%d ", arr[i]);
}
printf("\n");
getch();
}

# Implement Merge Sort and Quick sort to sort the given elements. Compare their time complexities. 
# Experiment no : 7

# MERGE SORT:
#include<stdio.h>
#include <stdlib.h>
#include<conio.h>
void merge(int arr[], int left, int mid, int right) {
int n1 = mid - left + 1;
int n2 = right - mid;
int L[n1], R[n2];
for (int i = 0; i < n1; i++)
L[i] = arr[left + i];
for (int j = 0; j < n2; j++)
R[j] = arr[mid + 1 + j];
int i = 0, j = 0, k = left;
while (i < n1 && j < n2) {
if (L[i] <= R[j]) {
arr[k] = L[i];
i++;
} else {
arr[k] = R[j];
j++;
}
k++;
}
while (i < n1) {
arr[k] = L[i];
i++;
k++;
}
while (j < n2) {
arr[k] = R[j];
j++;
k++;
}
}
void mergeSort(int arr[], int left, int right) {
if (left < right) {
int mid = left + (right - left) / 2;
mergeSort(arr, left, mid);
mergeSort(arr, mid + 1, right);
merge(arr, left, mid, right);
}
}
int main() {
int n;
printf("Enter number of elements: ");
scanf("%d", &n);
int arr[n]; printf("Enter elements:\n");
for (int i = 0; i < n; i++) {
scanf("%d", &arr[i]);
}
mergeSort(arr, 0, n - 1);
printf("Sorted array:\n");
for (int i = 0; i < n; i++) {
printf("%d ", arr[i]);
}
printf("\n");
getch();
}
Output:
Enter number of elements: 4
Enter elements:
7 14 6 12
Sorted array: 6
7 12 14

# QUICK SORT:
#include <stdio.h>
#include<conio.h>
void swap(int* a, int* b) {
int t = *a;
*a = *b;
*b = t;
}
int partition(int arr[], int low, int high) {
int pivot = arr[high];
int i = (low - 1);
for (int j = low; j < high; j++) {
if (arr[j] <= pivot) {
i++;
swap(&arr[i], &arr[j]);
}
}
swap(&arr[i + 1], &arr[high]);
return (i + 1);
}
void quickSort(int arr[], int low, int high) {
if (low < high) {
int pi = partition(arr, low, high);
quickSort(arr, low, pi - 1);
quickSort(arr, pi + 1, high);
}
}
int main() {
int n;
printf("Enter number of elements: ");
scanf("%d", &n);
int arr[n]; printf("Enter elements:\n");
for (int i = 0; i < n; i++) {
scanf("%d", &arr[i]);
}
 quickSort(arr, 0, n - 1);
printf("Sorted array:\n");
for (int i = 0; i < n; i++) {
printf("%d ", arr[i]);
}
printf("\n");
getch();
}
Output:
Enter number of elements: 7 Enter
elements:
4 364 243 67 568 132 74
Sorted array:
4 67 74 132 243 364 568

# Implement a binary search tree (BST) to perform insertion, deletion, and search operations.
# Experiment no : 8

#include<stdio.h>
#include <stdlib.h>
#include<conio.h>
// Structure of a BST node
struct TreeNode {
int key;
struct TreeNode *left, *right;
};
// Function to create a new BST node
struct TreeNode* newNode(int item) {
struct TreeNode* temp = (struct TreeNode*)malloc(sizeof(struct TreeNode));
temp->key = item;
temp->left = temp->right = NULL;
return temp;
}
// Function to insert a new key in BST
struct TreeNode* insert(struct TreeNode* node, int key) {
// If the tree is empty, return a new node
if (node == NULL) return newNode(key);
// Otherwise, recur down the tree
if (key < node->key)
node->left = insert(node->left, key);
else if (key > node->key)
node->right = insert(node->right, key);
// return the (unchanged) node pointer
return node;
}
// Function to perform inorder traversal of BST
void inorder(struct TreeNode* root) {
if (root != NULL) {
inorder(root->left);
printf("%d ", root->key);
inorder(root->right);
}
}
// Function to search a given key in BST
struct TreeNode* search(struct TreeNode* root, int key) {
// Base Cases: root is null or key is present at root
if (root == NULL || root->key == key)
return root;
// Key is greater than root's key
if (root->key < key)
return search(root->right, key);
// Key is smaller than root's key
return search(root->left, key);
}
// Function to find the minimum value node in a given BST
struct TreeNode* minValueNode(struct TreeNode* node) {
struct TreeNode* current = node;
// Loop down to find the leftmost leaf
while (current && current->left != NULL)
current = current->left;
return current;
}
// Function to delete a node with given key from BST struct TreeNode* deleteNode(struct
TreeNode* root, int key) {
// Base case
if (root == NULL) return root;
// Recur down the tree
if (key < root->key)
root->left = deleteNode(root->left, key);
else if (key > root->key)
root->right = deleteNode(root->right, key);
// If key is same as root's key, then This is the node to be deleted
else {
// Node with only one child or no child
if (root->left == NULL) {
struct TreeNode* temp = root->right;
free(root);
return temp;
} else if (root->right == NULL) {
struct TreeNode* temp = root->left;
free(root);
return temp;
}
// Node with two children: Get the inorder successor (smallest in the right subtree)
struct TreeNode* temp = minValueNode(root->right);
// Copy the inorder successor's content to this node
root->key = temp->key;
// Delete the inorder successor
root->right = deleteNode(root->right, temp->key);
}
return root;
}
// Main function to test the above functions
int main() {
struct TreeNode* root = NULL;
root = insert(root, 50);
root = insert(root, 30);
root = insert(root, 20);
root = insert(root, 40);
root = insert(root, 70);
root = insert(root, 60);
root = insert(root, 80);
printf("Inorder traversal of the given tree \n");
inorder(root);
printf("\nDelete 20\n");
root = deleteNode(root, 20);
printf("Inorder traversal of the modified tree \n");
inorder(root);
printf("\nDelete 30\n");
root = deleteNode(root, 30);
printf("Inorder traversal of the modified tree \n");
inorder(root);
printf("\nDelete 50\n");
root = deleteNode(root, 50);
printf("Inorder traversal of the modified tree \n");
inorder(root);
struct TreeNode* searchResult = search(root, 70);
if (searchResult != NULL)
printf("\nFound key 70 in the tree\n");
else
printf("\nKey 70 not found in the tree\n");
getch();
}
Output:
Inorder traversal of the given tree
20 30 40 50 60 70 80
Delete 20
Inorder traversal of the modified tree
30 40 50 60 70 80
Delete 30
Inorder traversal of the modified tree
 40 50 60 70 80
Delete 50
Inorder traversal of the modified tree
40 60 70 80
Found key 70 in the tree

# Implement graph traversal algorithms BFS and DFS...
# Experimnt no : 9

#include <stdio.h>
#include <stdlib.h>
#include<conio.h>
#define MAX 100
int adj[MAX][MAX]; int visited[MAX];
int queue[MAX], front = -1, rear = -1;
void enqueue(int v) { if (rear == MAX - 1) return;
if (front == -1) front = 0; queue[++rear] = v;
}
int dequeue() {
if (front == -1 || front > rear) return -1;
return queue[front++];
}
void bfs(int start, int n) {
int i;
enqueue(start);
visited[start] = 1;
while (front <= rear) {
int v = dequeue();
printf("%d ", v);
for (i = 0; i < n; i++) {
if (adj[v][i] && !visited[i]) {
enqueue(i);
visited[i] = 1;
}
}
}
}
int main() {
int n, i, j, start;
printf("Enter the number of vertices: ");
scanf("%d", &n);
printf("Enter the adjacency matrix:\n");
for (i = 0; i < n; i++)
for (j = 0; j < n; j++)
scanf("%d", &adj[i][j]);
printf("Enter the starting vertex: ");
scanf("%d", &start);
for (i = 0; i < n; i++) visited[i] = 0;
printf("BFS Traversal starting from vertex %d: ", start);
bfs(start, n);
getch();
}
DFS in C
c
Copy code
#include <stdio.h>
#include <stdlib.h>
#include<conio.h>
#define MAX 100
int adj[MAX][MAX]; int visited[MAX];
void dfs(int v, int n) {
int i;
printf("%d ", v);
visited[v] = 1; for (i = 0; i < n; i++) {
if (adj[v][i] && !visited[i]) {
dfs(i, n);
}
}
}
int main() {
int n, i, j, start;
printf("Enter the number of vertices: ");
scanf("%d", &n);
printf("Enter the adjacency matrix:\n");
for (i = 0; i < n; i++)
for (j = 0; j < n; j++)
scanf("%d", &adj[i][j]);
printf("Enter the starting vertex: ");
scanf("%d", &start);
for (i = 0; i < n; i++) visited[i] = 0;
printf("DFS Traversal starting from vertex %d: ", start);
dfs(start, n);
getch();
}




