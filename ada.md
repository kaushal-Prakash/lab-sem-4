# ADA LAB SEM 4

## 1. Selection Sort

### Comparison-based Sorting Algorithm

#### **Technique**
Selection Sort is a comparison-based sorting algorithm. It sorts an array by repeatedly selecting the minimum (or maximum) element from the unsorted region and swapping it with the first element of the unsorted region.

#### **Space Complexity**

$$
O(n)
$$

For storing the elements of the array.

#### **Time Complexity**

$$
O(n^2)
$$

For all cases, since comparisons are always performed, even if the array is already sorted.

#### **Code**
```c
#include <stdio.h>

void sort(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        int min = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[min]) min = j;
        }

        if (min != i) {
            int temp = arr[i];
            arr[i] = arr[min];
            arr[min] = temp;
        }
    }

    // Print sorted array
    printf("Sorted array using Selection Sort:\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int arr[] = {64, 25, 12, 22, 11};
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Original array:\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    sort(arr, n);

    return 0;
}
```
## 2. Quick Sort

### A Divide and Conquer Algorithm

#### **Technique**
Quick Sort is a divide and conquer algorithm. It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, according to whether they are less than or greater than the pivot. The sub-arrays are then sorted recursively.

#### **Space Complexity**

$$
O(\log n)
$$

On average, due to recursive function call stack (for in-place implementation).

#### **Time Complexity**

- **Best Case:**  
$$
O(n \log n)
$$

- **Average Case:**  
$$
O(n \log n)
$$

- **Worst Case (already sorted or all equal):**  
$$
O(n^2)
$$

#### **Code**
```c
#include <stdio.h>

// Function to swap two elements
void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Partition function
int partition(int arr[], int low, int high) {
    int pivot = arr[high]; // Choosing the last element as pivot
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }

    swap(&arr[i + 1], &arr[high]);
    return i + 1;
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);

        // Recursively sort elements before and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = { 10, 7, 8, 9, 1, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Original array:\n");
    printArray(arr, n);

    quickSort(arr, 0, n - 1);

    printf("Sorted array using Quick Sort:\n");
    printArray(arr, n);

    return 0;
}
```
Still have a doubt ? [Click here](https://www.youtube.com/watch?v=WIrA4YexLRQ&t=1943s)

## 3. Merge Sort

### A Divide and Conquer Algorithm

#### **Technique**
Merge Sort is a classic divide and conquer sorting algorithm. It works by recursively splitting the array into halves until each sub-array has one element, and then merging the sorted sub-arrays back together.

#### **Space Complexity**

$$
O(n)
$$

Because it uses additional arrays to store temporary results during merging.

#### **Time Complexity**

- **Best Case:**  
$$
O(n \log n)
$$

- **Average Case:**  
$$
O(n \log n)
$$

- **Worst Case:**  
$$
O(n \log n)
$$

#### **Code**
```c
#include <stdio.h>

// Function to merge two sorted halves
void merge(int arr[], int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;

    int L[n1], R[n2];

    // Copy data to temp arrays
    for (int i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    // Merge the temp arrays back into arr[l..r]
    int i = 0, j = 0, k = l;

    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k++] = L[i++];
        } else {
            arr[k++] = R[j++];
        }
    }

    // Copy remaining elements
    while (i < n1)
        arr[k++] = L[i++];
    while (j < n2)
        arr[k++] = R[j++];
}

void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;

        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);

        merge(arr, l, m, r);
    }
}

void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = {12, 11, 13, 5, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Original array:\n");
    printArray(arr, n);

    mergeSort(arr, 0, n - 1);

    printf("Sorted array using Merge Sort:\n");
    printArray(arr, n);

    return 0;
}
```
## 4. Topological Sorting 
It is a sorting algorithm for directed acyclic graph(DAG). It linearly orders the vertices such that for every directed edge
$$
u -> v
$$
u comes before v in the ordering.

### **Technique**
we use a **queue** initialized with a start vertex (like 0) and an **indegree array**. We remove a node from queue (using dequeue method), add it to result (array) and get its neighbours, then we traverse through them and decrease their indegree by one & if its zero we add them back to queue.

### **Applications**
Arranging course structure of college.

### **Time Complexity**
$$
O(V + E)
$$
for all cases.

### **Space Complexity**
$$
O(V)
$$
to store the resultant array

### **Code**
```c
#include <stdio.h>
#include <stdlib.h>

#define MAX 100

// Adjacency list node
typedef struct Node {
    int vertex;
    struct Node* next;
} Node;

// Queue structure
typedef struct {
    int items[MAX];
    int front, rear;
} Queue;

Queue* createQueue() {
    Queue* q = malloc(sizeof(Queue));
    q->front = -1;
    q->rear = -1;
    return q;
}

int isEmpty(Queue* q) {
    return q->front == -1;
}

void enqueue(Queue* q, int value) {
    if (q->rear == MAX - 1) return;
    if (isEmpty(q)) q->front = 0;
    q->items[++q->rear] = value;
}

int dequeue(Queue* q) {
    if (isEmpty(q)) return -1;
    int item = q->items[q->front];
    if (q->front == q->rear)
        q->front = q->rear = -1;
    else
        q->front++;
    return item;
}

// Graph structure
Node* adj[MAX];
int indegree[MAX];

void addEdge(int u, int v) {
    Node* newNode = malloc(sizeof(Node));
    newNode->vertex = v;
    newNode->next = adj[u];
    adj[u] = newNode;
}

void topologicalSort(int V) {
    Queue* q = createQueue();

    // Enqueue all vertices with indegree 0
    for (int i = 0; i < V; i++) {
        if (indegree[i] == 0)
            enqueue(q, i);
    }

    int count = 0;
    int result[MAX];

    while (!isEmpty(q)) {
        int node = dequeue(q);
        result[count++] = node;

        for (Node* temp = adj[node]; temp != NULL; temp = temp->next) {
            indegree[temp->vertex]--;
            if (indegree[temp->vertex] == 0)
                enqueue(q, temp->vertex);
        }
    }

    if (count != V) {
        printf("Cycle detected! Topological sort not possible.\n");
    } else {
        printf("Topological Order: ");
        for (int i = 0; i < count; i++)
            printf("%d ", result[i]);
        printf("\n");
    }
}

int main() {
    int V = 6; // Number of vertices

    // Initialize adjacency list and indegree array
    for (int i = 0; i < V; i++) {
        adj[i] = NULL;
        indegree[i] = 0;
    }

    // Add edges and update indegree
    addEdge(0, 1); indegree[1]++;
    addEdge(0, 2); indegree[2]++;
    addEdge(1, 3); indegree[3]++;
    addEdge(2, 3); indegree[3]++;
    addEdge(3, 4); indegree[4]++;
    addEdge(4, 5); indegree[5]++;

    topologicalSort(V);

    return 0;
}
```
