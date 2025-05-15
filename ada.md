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
