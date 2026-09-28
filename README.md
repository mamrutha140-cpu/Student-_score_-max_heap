# Student-_score_-max_heap
Student Score Maximum: Max Heap vs Linear Search

1. Aim

To implement a Max Heap and Linear Search in C to find the highest student score, record the intermediate steps, count comparisons/operations, and compare the performance of both approaches.

---

2. Input Data

78 92 65 88 95 72 84 90

Number of students = 8

---

3. C Program

#include <stdio.h>

#define MAX 100

int heap[MAX];
int heapSize = 0;

int heapComparisons = 0;
int linearComparisons = 0;

void printHeap(void)
{
    int i;

    printf("[ ");

    for (i = 0; i < heapSize; i++)
    {
        printf("%d ", heap[i]);
    }

    printf("]\n");
}

void insertHeap(int value)
{
    int i;
    int parent;
    int temp;

    heap[heapSize] = value;
    i = heapSize;
    heapSize++;

    while (i > 0)
    {
        parent = (i - 1) / 2;

        heapComparisons++;

        if (heap[parent] >= heap[i])
        {
            break;
        }

        temp = heap[parent];
        heap[parent] = heap[i];
        heap[i] = temp;

        i = parent;
    }
}

int findMaxHeap(void)
{
    return heap[0];
}

int linearSearchMax(int arr[], int n)
{
    int max = arr[0];
    int i;

    linearComparisons = 0;

    for (i = 1; i < n; i++)
    {
        linearComparisons++;

        if (arr[i] > max)
        {
            max = arr[i];
        }
    }

    return max;
}

int main(void)
{
    int scores[] = {78, 92, 65, 88, 95, 72, 84, 90};
    int n = sizeof(scores) / sizeof(scores[0]);

    int i;
    int maxHeapResult;
    int linearResult;

    printf("========================================\n");
    printf("       MAX HEAP vs LINEAR SEARCH\n");
    printf("========================================\n\n");

    printf("Input Scores:\n");

    for (i = 0; i < n; i++)
    {
        printf("%d ", scores[i]);
    }

    printf("\n\n");

    printf("MAX HEAP INSERTION TRACE\n");
    printf("------------------------\n");

    for (i = 0; i < n; i++)
    {
        insertHeap(scores[i]);

        printf("After inserting %d: ", scores[i]);
        printHeap();
    }

    printf("\nTotal heap insertion comparisons = %d\n",
           heapComparisons);

    maxHeapResult = findMaxHeap();

    printf("\nMAX HEAP SEARCH\n");
    printf("Maximum score = %d\n", maxHeapResult);
    printf("Comparisons required = 0\n");
    printf("Root access operation = 1\n");

    linearResult = linearSearchMax(scores, n);

    printf("\nLINEAR SEARCH\n");
    printf("Maximum score = %d\n", linearResult);
    printf("Comparisons required = %d\n",
           linearComparisons);

    printf("\n========================================\n");
    printf("             FINAL RESULTS\n");
    printf("========================================\n");

    printf("Max Heap maximum        : %d\n",
           maxHeapResult);

    printf("Max Heap comparisons    : 0\n");

    printf("Linear Search maximum   : %d\n",
           linearResult);

    printf("Linear comparisons      : %d\n",
           linearComparisons);

    printf("Heap insertion compares : %d\n",
           heapComparisons);

    return 0;
}

---

4. Program Output

========================================
       MAX HEAP vs LINEAR SEARCH
========================================

Input Scores:
78 92 65 88 95 72 84 90

MAX HEAP INSERTION TRACE
------------------------
After inserting 78: [ 78 ]
After inserting 92: [ 92 78 ]
After inserting 65: [ 92 78 65 ]
After inserting 88: [ 92 88 65 78 ]
After inserting 95: [ 95 92 65 78 88 ]
After inserting 72: [ 95 92 65 78 88 72 ]
After inserting 84: [ 95 92 84 78 88 72 65 ]
After inserting 90: [ 95 90 84 92 88 72 65 78 ]

Total heap insertion comparisons = 9

MAX HEAP SEARCH
Maximum score = 95
Comparisons required = 0
Root access operation = 1

LINEAR SEARCH
Maximum score = 95
Comparisons required = 7

========================================
             FINAL RESULTS
========================================
Max Heap maximum        : 95
Max Heap comparisons    : 0
Linear Search maximum   : 95
Linear comparisons      : 7
Heap insertion compares : 9

---

5. Max Heap Trace Table

Step| Inserted Score| Heap Arrangement| Comparisons
1| 78| "[78]"| 0
2| 92| "[92, 78]"| 1
3| 65| "[92, 78, 65]"| 1
4| 88| "[92, 88, 65, 78]"| 1
5| 95| "[95, 92, 65, 78, 88]"| 2
6| 72| "[95, 92, 65, 78, 88, 72]"| 1
7| 84| "[95, 92, 84, 78, 88, 72, 65]"| 1
8| 90| "[95, 90, 84, 92, 88, 72, 65, 78]"| 2
Total| | | 9

---

6. Final Max Heap

             95
           /    \
         90      84
        /  \    /  \
      92   88  72   65
     /
    78

The highest score 95 is stored at the root.

---

7. Linear Search Trace Table

Step| Score Checked| Current Maximum| Comparison
Start| 78| 78| Initial value
1| 92| 92| 92 > 78
2| 65| 92| 65 > 92 → No
3| 88| 92| 88 > 92 → No
4| 95| 95| 95 > 92
5| 72| 95| 72 > 95 → No
6| 84| 95| 84 > 95 → No
7| 90| 95| 90 > 95 → No

Total comparisons:

7

Maximum score:

95

---

8. Performance Comparison

Operation| Max Heap| Linear Search
Find maximum| O(1)| O(n)
Given-data comparisons| 0 key comparisons| 7
Root access| 1 operation| Not applicable
Insert new score| O(log n) worst case| O(1)*
Additional space| O(n)| O(1)
Repeated maximum queries| Efficient| O(n) for each search

"*" Appending a new score is O(1) when array capacity is available.

---

9. Complexity Analysis

Max Heap

Finding Maximum

The maximum is always at the root.

Time Complexity: O(1)

Insertion

A newly inserted score may move upward through the heap.

Worst-case Time Complexity: O(log n)

Space

The heap stores all student scores.

Space Complexity: O(n)

---

Linear Search

Finding Maximum

Every score must be examined.

For "n" scores:

Number of comparisons = n - 1

For 8 scores:

8 - 1 = 7 comparisons

Time Complexity: O(n)

Space

Only a variable is required to store the current maximum.

Additional Space Complexity: O(1)

---

10. Increasing Number of Students

Number of Students| Linear Search Comparisons| Max Heap Maximum Access
8| 7| 1 root access
100| 99| 1 root access
1,000| 999| 1 root access
10,000| 9,999| 1 root access

Linear Search becomes more expensive as the number of students increases.

A Max Heap continues to provide O(1) access to the current maximum.

---

11. Inserting a New Score

Suppose a new score 97 is inserted.

Before insertion:

[95, 90, 84, 92, 88, 72, 65, 78]

After inserting 97:

[95, 90, 84, 92, 88, 72, 65, 78, 97]

After restoring the Max Heap property:

[97, 95, 84, 90, 88, 72, 65, 78, 92]

The insertion may require the new score to move upward.

Worst-case complexity = O(log n)

---

12. Analysis

For Linear Search:

Insert → O(1)
Find Maximum → O(n)

For Max Heap:

Insert → O(log n)
Find Maximum → O(1)

Linear Search is simple and requires no additional data structure, but every time the maximum is requested, the scores must be scanned.

The Max Heap requires additional memory and more work during insertion, but the maximum is immediately available at the root.

---

13. Final Conclusion

Both methods correctly identify the highest student score:

Highest Score = 95

For the given 8 scores:

- Max Heap maximum access = 1 root-access operation
- Max Heap key comparisons for finding maximum = 0
- Linear Search comparisons = 7
- Total heap insertion comparisons = 9

A Max Heap is suitable for continuously maintaining the highest score when new scores are added and the maximum is frequently requested.

The Max Heap provides:

- O(1) maximum access
- O(log n) worst-case insertion
- O(n) space

Linear Search provides:

- O(n) maximum search
- O(1) additional space

Therefore, for a university system that continuously receives student scores and frequently needs the highest score, the Max Heap approach is a suitable choice.
