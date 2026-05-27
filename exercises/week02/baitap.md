#include <iostream>
using namespace std;

void nhapMang(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        cout << "arr[" << i << "] = ";
        cin >> arr[i];
    }
}

void inMang(int arr[], int n) {
    cout << "Mang: ";
    for (int i = 0; i < n; i++) {
        cout << arr[i];
        if (i < n - 1) cout << ", ";
    }
    cout << endl;
}

int timMin(int arr[], int n) {
    int min = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] < min)
            min = arr[i];
    }
    return min;
}

int timMax(int arr[], int n) {
    int max = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > max)
            max = arr[i];
    }
    return max;
}

long long tinhTong(int arr[], int n) {
    long long tong = 0;
    for (int i = 0; i < n; i++)
        tong += arr[i];
    return tong;
}

double tinhTrungBinh(int arr[], int n) {
    return (double)tinhTong(arr, n) / n;
}

int main() {
    int n;
    cout << "Nhap so phan tu n: ";
    cin >> n;

    if (n <= 0) {
        cout << "n phai lon hon 0!" << endl;
        return 1;
    }

    int arr[1000]; // mảng tĩnh, tối đa 1000 phần tử
    nhapMang(arr, n);

    inMang(arr, n);

    cout << "Min     : " << timMin(arr, n)       << endl;
    cout << "Max     : " << timMax(arr, n)       << endl;
    cout << "Tong    : " << tinhTong(arr, n)     << endl;
    cout << "Trung binh: " << tinhTrungBinh(arr, n) << endl;

    return 0;
}
