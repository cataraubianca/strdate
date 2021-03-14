test 1:
#include <iostream>
#include <iomanip>
#include <stdlib.h>
#include <time.h>
#include <algorithm>
using namespace std;

/*Bubble Sort
T=1
N=1000
Max=100000

*/

void swap(int *a, int *b)
{
    int temp =*a;
    *a=*b;
    *b= temp;

}
void BubbleSort(int v[], int n)
{   int i,j;
    for(i=0;i<n-1;i++)
        for(j=0;j<n-i-1;j++)
            if(v[j]>v[j+1])
            swap(&v[j+1],&v[j]);
}
void CountingSort(int v[], int n) {
    int max = v[0];

    for (int i = 1; i < n; i++)
    {   if (v[i] > max)
        max = v[i];
    } 
    int fr[10];
    for (int i = 0; i <= max; ++i)
        fr[i] = 0;
    for (int i = 0; i < n; i++)
        fr[v[i]]++;
    for (int i = 1; i <= max; i++)
        fr[i] =fr[i] + fr[i - 1];
    int final [10];
    for (int i = n - 1; i >= 0; i--)
    {
        final[fr[v[i]] - 1] = v[i];
        fr[v[i]]--;
    }
    for (int i = 0; i < n; i++)
        v[i] = final[i];
}
void final(int v[], int l, int m, int r, int n)
{
    int i = l;
    int j = m + 1;
    int k = l;
    int prov[n];

    while (i <= m && j <= r) {
        if (v[i] <= v[j]) {
            prov[k] = v[i];
            i++;
            k++;
        }
        else {
            prov[k] = v[j];
            j++;
            k++;
        }
    }
    while (i <= m) {
        prov[k] = v[i];
        i++;
        k++;
    }

    while (j <= r) {
        prov[k] = v[j];
        j++;
        k++;
    }

    for (int p = l; p <= r; p++) {
        v[p] = prov[p];
    }
}

void MergeSort(int v[], int l, int r, int n)
{
    if (l < r) {
        int m = (l + r) / 2;
        MergeSort(v, l, m, n);
        MergeSort(v, m + 1, r, n);
        final(v, l, m, r, n);
    }
}
int piv(int v[], int i, int f){
    int pivot=v[f];
    int index=i;
    for(int j=i;j<f;j++)
     {
         if(v[j]<pivot){
                swap(v[j],v[index]);
                index++;
                }
     }
    swap (v[f],v[index]);
    return index;
}
void quicksort(int v[],int i,int f)
{
    if(i<f)
    {int p= piv(v,i,f);
    quicksort(v,i,(p-1));
    quicksort(v,(p+1),f);}

}
int getMax(int v[], int n)
{
  int max = v[0];
  for (int i = 1; i < n; i++)
    if (v[i] > max)
      max = v[i];
  return max;
}

void sortare(int v[], int n, int poz) {
    int max = v[0];

    for (int i = 1; i < n; i++)
    {   if (v[i] > max)
        max = v[i];
    }
    int fr[10];
    for (int i = 0; i <= max; ++i)
        fr[i] = 0;
    for (int i = 0; i < n; i++)
        fr[v[i]/poz%10]++;
    for (int i = 1; i <= max; i++)
        fr[i] =fr[i] + fr[i - 1];
    int final [10];
    for (int i = n - 1; i >= 0; i--)
    {
        final[fr[v[i]] - 1] = v[i];
        fr[v[i]]--;
    }
    for (int i = 0; i < n; i++)
        v[i] = final[i];
}

void radixsort(int v[], int n)
{
  int max = getMax(v, n);

  for (int poz = 1; max / poz > 0; poz *= 10)
    sortare(v, n, poz);
}

int main()

{ int arr[]={23,44,3,5,67,10453,10000,65,432,1234,85,4957,433,2234,5567,5432,2367,763,237,6,345,65,43,45,65,44,45};
int n=sizeof(arr)/sizeof(arr[0]);
    time_t start, end;
    time(&start);
    ios_base::sync_with_stdio(false);
    BubbleSort(arr,n);
    time(&end);
    double time_taken = double(end - start);
    cout << "Time taken by bubble sort is : " << fixed
         << time_taken << setprecision(6);
    cout << " sec " << endl;

    time_t start1, end1;
    time(&start1);
    ios_base::sync_with_stdio(false);
    BubbleSort(arr,n);
    time(&end1);
    double time_taken1 = double(end1 - start1);
    cout << "Time taken by counting sort is : " << fixed
         << time_taken1 << setprecision(6);
    cout << " sec " << endl;

    time_t start2, end2;
    time(&start2);
    ios_base::sync_with_stdio(false);
    MergeSort(arr, 0, (n - 1), n);
    time(&end2);
    double time_taken2 = double(end2 - start2);
    cout << "Time taken by merge sort is : " << fixed
         << time_taken2 << setprecision(6);
    cout << " sec " << endl;

    time_t start3, end3;
    time(&start3);
    ios_base::sync_with_stdio(false);
    quicksort(arr, 0, n);
    time(&end3);
    double time_taken3 = double(end3 - start3);
    cout << "Time taken by quick sort is : " << fixed
         << time_taken3 << setprecision(6);
    cout << " sec " << endl;

    time_t start4, end4;
    time(&start4);
    ios_base::sync_with_stdio(false);
    radixsort(arr,n);
    time(&end4);
    double time_taken4 = double(end4 - start4);
    cout << "Time taken by radix sort is : " << fixed
         << time_taken4 << setprecision(6);
    cout << " sec " << endl;


}

test 2:
#include <iostream>
#include <iomanip>
#include <stdlib.h>
#include <time.h>
#include <algorithm>
using namespace std;

/*
T=2
N=10000
Max=100

*/

void swap(int *a, int *b)
{
    int temp =*a;
    *a=*b;
    *b= temp;

}
void BubbleSort(int v[], int n)
{   int i,j;
    for(i=0;i<n-1;i++)
        for(j=0;j<n-i-1;j++)
            if(v[j]>v[j+1])
            swap(&v[j+1],&v[j]);
}
void CountingSort(int v[], int n) {
    int max = v[0];

    for (int i = 1; i < n; i++)
    {   if (v[i] > max)
        max = v[i];
    }
    int fr[10];
    for (int i = 0; i <= max; ++i)
        fr[i] = 0;
    for (int i = 0; i < n; i++)
        fr[v[i]]++;
    for (int i = 1; i <= max; i++)
        fr[i] =fr[i] + fr[i - 1];
    int final [10];
    for (int i = n - 1; i >= 0; i--)
    {
        final[fr[v[i]] - 1] = v[i];
        fr[v[i]]--;
    }
    for (int i = 0; i < n; i++)
        v[i] = final[i];
}
void final(int v[], int l, int m, int r, int n)
{
    int i = l;
    int j = m + 1;
    int k = l;
    int prov[n];

    while (i <= m && j <= r) {
        if (v[i] <= v[j]) {
            prov[k] = v[i];
            i++;
            k++;
        }
        else {
            prov[k] = v[j];
            j++;
            k++;
        }
    }
    while (i <= m) {
        prov[k] = v[i];
        i++;
        k++;
    }

    while (j <= r) {
        prov[k] = v[j];
        j++;
        k++;
    }

    for (int p = l; p <= r; p++) {
        v[p] = prov[p];
    }
}

void MergeSort(int v[], int l, int r, int n)
{
    if (l < r) {
        int m = (l + r) / 2;
        MergeSort(v, l, m, n);
        MergeSort(v, m + 1, r, n);
        final(v, l, m, r, n);
    }
}
int piv(int v[], int i, int f){
    int pivot=v[f];
    int index=i;
    for(int j=i;j<f;j++)
     {
         if(v[j]<pivot){
                swap(v[j],v[index]);
                index++;
                }
     }
    swap (v[f],v[index]);
    return index;
}
void quicksort(int v[],int i,int f)
{
    if(i<f)
    {int p= piv(v,i,f);
    quicksort(v,i,(p-1));
    quicksort(v,(p+1),f);}

}
int getMax(int v[], int n)
{
  int max = v[0];
  for (int i = 1; i < n; i++)
    if (v[i] > max)
      max = v[i];
  return max;
}

void sortare(int v[], int n, int poz) {
    int max = v[0];

    for (int i = 1; i < n; i++)
    {   if (v[i] > max)
        max = v[i];
    }
    int fr[10];
    for (int i = 0; i <= max; ++i)
        fr[i] = 0;
    for (int i = 0; i < n; i++)
        fr[v[i]/poz%10]++;
    for (int i = 1; i <= max; i++)
        fr[i] =fr[i] + fr[i - 1];
    int final [10];
    for (int i = n - 1; i >= 0; i--)
    {
        final[fr[v[i]] - 1] = v[i];
        fr[v[i]]--;
    }
    for (int i = 0; i < n; i++)
        v[i] = final[i];
}

void radixsort(int v[], int n)
{
  int max = getMax(v, n);

  for (int poz = 1; max / poz > 0; poz *= 10)
    sortare(v, n, poz);
}

int main()

{ int arr[]={23,44,3,5,67,10453,100000,65,432,1234,85,4957,433,2234,34,56,78,765,4323,456,234,567,654,32,123,456,543,4,56,7,5567,5432,2367,763,237,6,345,65,43,45,65,44,45};
int n=sizeof(arr)/sizeof(arr[0]);
    time_t start, end;
    time(&start);
    ios_base::sync_with_stdio(false);
    BubbleSort(arr,n);
    time(&end);
    double time_taken = double(end - start);
    cout << "Time taken by bubble sort is : " << fixed
         << time_taken << setprecision(6);
    cout << " sec " << endl;

    time_t start1, end1;
    time(&start1);
    ios_base::sync_with_stdio(false);
    BubbleSort(arr,n);
    time(&end1);
    double time_taken1 = double(end1 - start1);
    cout << "Time taken by counting sort is : " << fixed
         << time_taken1 << setprecision(6);
    cout << " sec " << endl;

    time_t start2, end2;
    time(&start2);
    ios_base::sync_with_stdio(false);
    MergeSort(arr, 0, (n - 1), n);
    time(&end2);
    double time_taken2 = double(end2 - start2);
    cout << "Time taken by merge sort is : " << fixed
         << time_taken2 << setprecision(6);
    cout << " sec " << endl;

    time_t start3, end3;
    time(&start3);
    ios_base::sync_with_stdio(false);
    quicksort(arr, 0, n);
    time(&end3);
    double time_taken3 = double(end3 - start3);
    cout << "Time taken by quick sort is : " << fixed
         << time_taken3 << setprecision(6);
    cout << " sec " << endl;

    time_t start4, end4;
    time(&start4);
    ios_base::sync_with_stdio(false);
    radixsort(arr,n);
    time(&end4);
    double time_taken4 = double(end4 - start4);
    cout << "Time taken by radix sort is : " << fixed
         << time_taken4 << setprecision(6);
    cout << " sec " << endl;


}

test 3:
#include <iostream>
#include <iomanip>
#include <stdlib.h>
#include <time.h>
#include <algorithm>
using namespace std;

/*Bubble Sort
T=3
N=1000
Max=100000

*/

void swap(int *a, int *b)
{
    int temp =*a;
    *a=*b;
    *b= temp;

}
void BubbleSort(int v[], int n)
{   int i,j;
    for(i=0;i<n-1;i++)
        for(j=0;j<n-i-1;j++)
            if(v[j]>v[j+1])
            swap(&v[j+1],&v[j]);
}
void CountingSort(int v[], int n) {
    int max = v[0];

    for (int i = 1; i < n; i++)
    {   if (v[i] > max)
        max = v[i];
    }
    int fr[10];
    for (int i = 0; i <= max; ++i)
        fr[i] = 0;
    for (int i = 0; i < n; i++)
        fr[v[i]]++;
    for (int i = 1; i <= max; i++)
        fr[i] =fr[i] + fr[i - 1];
    int final [10];
    for (int i = n - 1; i >= 0; i--)
    {
        final[fr[v[i]] - 1] = v[i];
        fr[v[i]]--;
    }
    for (int i = 0; i < n; i++)
        v[i] = final[i];
}
void final(int v[], int l, int m, int r, int n)
{
    int i = l;
    int j = m + 1;
    int k = l;
    int prov[n];

    while (i <= m && j <= r) {
        if (v[i] <= v[j]) {
            prov[k] = v[i];
            i++;
            k++;
        }
        else {
            prov[k] = v[j];
            j++;
            k++;
        }
    }
    while (i <= m) {
        prov[k] = v[i];
        i++;
        k++;
    }

    while (j <= r) {
        prov[k] = v[j];
        j++;
        k++;
    }

    for (int p = l; p <= r; p++) {
        v[p] = prov[p];
    }
}

void MergeSort(int v[], int l, int r, int n)
{
    if (l < r) {
        int m = (l + r) / 2;
        MergeSort(v, l, m, n);
        MergeSort(v, m + 1, r, n);
        final(v, l, m, r, n);
    }
}
int piv(int v[], int i, int f){
    int pivot=v[f];
    int index=i;
    for(int j=i;j<f;j++)
     {
         if(v[j]<pivot){
                swap(v[j],v[index]);
                index++;
                }
     }
    swap (v[f],v[index]);
    return index;
}
void quicksort(int v[],int i,int f)
{
    if(i<f)
    {int p= piv(v,i,f);
    quicksort(v,i,(p-1));
    quicksort(v,(p+1),f);}

}
int getMax(int v[], int n)
{
  int max = v[0];
  for (int i = 1; i < n; i++)
    if (v[i] > max)
      max = v[i];
  return max;
}

void sortare(int v[], int n, int poz) {
    int max = v[0];

    for (int i = 1; i < n; i++)
    {   if (v[i] > max)
        max = v[i];
    }
    int fr[10];
    for (int i = 0; i <= max; ++i)
        fr[i] = 0;
    for (int i = 0; i < n; i++)
        fr[v[i]/poz%10]++;
    for (int i = 1; i <= max; i++)
        fr[i] =fr[i] + fr[i - 1];
    int final [10];
    for (int i = n - 1; i >= 0; i--)
    {
        final[fr[v[i]] - 1] = v[i];
        fr[v[i]]--;
    }
    for (int i = 0; i < n; i++)
        v[i] = final[i];
}

void radixsort(int v[], int n)
{
  int max = getMax(v, n);

  for (int poz = 1; max / poz > 0; poz *= 10)
    sortare(v, n, poz);
}

int main()

{ int arr[]={23,44,3,5,67,10453,100000,65,432,1234,85,4957,433,2234,5567,5432,2367,763,237,6,345,65,43,45,5567,5432,2367,763,237,6,345,65,43,45,65,44,45};
int n=sizeof(arr)/sizeof(arr[0]);
    time_t start, end;
    time(&start);
    ios_base::sync_with_stdio(false);
    BubbleSort(arr,n);
    time(&end);
    double time_taken = double(end - start);
    cout << "Time taken by bubble sort is : " << fixed
         << time_taken << setprecision(6);
    cout << " sec " << endl;

    time_t start1, end1;
    time(&start1);
    ios_base::sync_with_stdio(false);
    BubbleSort(arr,n);
    time(&end1);
    double time_taken1 = double(end1 - start1);
    cout << "Time taken by counting sort is : " << fixed
         << time_taken1 << setprecision(6);
    cout << " sec " << endl;

    time_t start2, end2;
    time(&start2);
    ios_base::sync_with_stdio(false);
    MergeSort(arr, 0, (n - 1), n);
    time(&end2);
    double time_taken2 = double(end2 - start2);
    cout << "Time taken by merge sort is : " << fixed
         << time_taken2 << setprecision(6);
    cout << " sec " << endl;

    time_t start3, end3;
    time(&start3);
    ios_base::sync_with_stdio(false);
    quicksort(arr, 0, n);
    time(&end3);
    double time_taken3 = double(end3 - start3);
    cout << "Time taken by quick sort is : " << fixed
         << time_taken3 << setprecision(6);
    cout << " sec " << endl;

    time_t start4, end4;
    time(&start4);
    ios_base::sync_with_stdio(false);
    radixsort(arr,n);
    time(&end4);
    double time_taken4 = double(end4 - start4);
    cout << "Time taken by radix sort is : " << fixed
         << time_taken4 << setprecision(6);
    cout << " sec " << endl;

    return 0;
}
