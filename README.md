#include <iostream>
using namespace std;

void sumAndProduct(int* arr, int size, int* sum, int* product) {
    *sum = 0;
    *product = 1;
    for (int i = 0; i < size; i++) {
        *sum += arr[i];
        *product *= arr[i];
    }
}

void countElements(int* arr, int size, int* neg, int* pos, int* zero) {
    *neg = *pos = *zero = 0;
    for (int i = 0; i < size; i++) {
        if (arr[i] < 0) (*neg)++;
        else if (arr[i] > 0) (*pos)++;
        else (*zero)++;
    }
}

int* append(int* arr, int& size, int* staticArr, int staticArrSize) {
    int newSize = size + staticArrSize;
    int* newArr = new int[newSize];

    for (int i = 0; i < size; i++)
        newArr[i] = arr[i];

    for (int i = 0; i < staticArrSize; i++)
        newArr[size + i] = staticArr[i];

    delete[] arr;
    size = newSize;
    return newArr;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = 5;

    cout << "task 1\n";
    int sum, product;
    sumAndProduct(arr, size, &sum, &product);
    cout << "sum: " << sum << "\n";
    cout << "product: " << product << "\n\n";

    cout << "task 2\n";
    int neg, pos, zero;
    countElements(arr, size, &neg, &pos, &zero);
    cout << "negative: " << neg << "\n";
    cout << "positive: " << pos << "\n";
    cout << "zero: " << zero << "\n\n";

    cout << "task 5\n";
    int staticArrSize = 3;
    int staticArr[] = {7, 8, 9};

    int* dynamic = new int[size];
    for (int i = 0; i < size; i++) {
        dynamic[i] = arr[i];
    }

    dynamic = append(dynamic, size, staticArr, staticArrSize);

    cout << "updated array: ";
    for (int i = 0; i < size; i++) {
        cout << dynamic[i] << " ";
    }
    cout << "\n";

    delete[] dynamic;
    return 0;
}

