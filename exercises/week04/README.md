# Tuần 4: Sắp Xếp Cơ Bản — Bài tập

## 🎯 Mục tiêu tuần này
Cài đặt và hiểu Bubble Sort, Selection Sort, Insertion Sort.

---

### Bài 1: Cài đặt 3 thuật toán ⭐⭐
Bubble Sort, Selection Sort, Insertion Sort. Mỗi cái in từng bước thay đổi mảng.

#include <iostream>
using namespace std;

const int MAX = 100;

void nhapmang(int a[], int n) {
    for (int i = 0; i < n; i++) {
        cout << "a[" << i << "] =";
        cin >> a[i];
    }
}


void xuatmang(int a[], int n) {
    for (int i = 0; i < n; i++) {
        cout << a[i] << " ";
    }
    cout << endl;
}


void bubbleSort(int a[], int n) {
    cout << "\n--- Bat dau Bubble Sort ---" << endl;
    for (int i = 0; i < n - 1; i++) {
        bool swapped = false;
        for (int j = 0; j < n - i - 1; j++) {
            if (a[j] > a[j + 1]) {

                int temp = a[j];
                a[j] = a[j + 1];
                a[j + 1] = temp;
                swapped = true;

                cout << "Hoan doi (" << a[j + 1] << " <-> " << a[j] << "): ";
                xuatmang(a, n);
            }
        }
        if (!swapped) break; 
    }
}


void selectionSort(int a[], int n) {
    cout << "\n--- Bat dau Selection Sort ---" << endl;
    for (int i = 0; i < n - 1; i++) {
        int min_idx = i;
        for (int j = i + 1; j < n; j++) {
            if (a[j] < a[min_idx]) {
                min_idx = j;
            }
        }
        if (min_idx != i) {
            int temp = a[i];
            a[i] = a[min_idx];
            a[min_idx] = temp;
            cout << "Dua " << a[i] << " (min) ve vi tri " << i << ": ";
        }
        else {
            cout << "Vi tri " << i << " da la nho nhat trong doan con lai: ";
        }
        xuatmang(a, n);
    }
}

void insertionSort(int a[], int n) {
    cout << "\n--- Bat dau Insertion Sort ---" << endl;
    for (int i = 1; i < n; i++) {
        int key = a[i];
        int j = i - 1;

        while (j >= 0 && a[j] > key) {
            a[j + 1] = a[j];
            j = j - 1;
        }
        a[j + 1] = key;

        cout << "Chen " << key << " vao vi tri thich hop: ";
        xuatmang(a, n);
    }
}

int main() {
    int n;
    int a[MAX];

    cout << "nhap kich thuoc mang: ";
    cin >> n;

    nhapmang(a, n);

    cout << "Chon thuat toan de sap xep:" << endl;
    cout << "1. Bubble Sort" << endl;
    cout << "2. Selection Sort" << endl;
    cout << "3. Insertion Sort" << endl;
    cout << "nhap lua chon (1-3): ";

    int choice;
    cin >> choice;
    

    if (choice == 1) {
        bubbleSort(a, n);
    }
    else if (choice == 2) {
        selectionSort(a, n);
    }
    else if (choice == 3) {
        insertionSort(a, n);
    }
    else {
        cout << " nhap tu 1 den 3." << endl;
        return 1;
    }
        

    cout << "Ket qua : ";
    xuatmang(a, n);

    return 0;
}

### Bài 2: Đếm số phép so sánh và hoán vị ⭐⭐
Với cùng 1 mảng 100 phần tử: đếm số lần so sánh và số lần hoán vị của 3 thuật toán. In bảng so sánh.

### Bài 3: Best / Worst / Average Case ⭐⭐
Với mảng đã sắp xếp, ngược chiều, và ngẫu nhiên — đo thời gian chạy 3 thuật toán. Kết luận khi nào nên dùng cái nào.

### Bài 4: 🔥 Dự Án Mini — Sorting Visualizer (Console) ⭐⭐⭐
> **Cảm hứng:** [Sorting — algorithm-visualizer.org](https://algorithm-visualizer.org/simple-recursive/bubble-sort)

Hiển thị từng bước sắp xếp trực quan bằng thanh ASCII:
```
Bubble Sort — Bước 3/8:
█████████████████ 17
████████████ 12
██████████████████████ 22
████████ 8
███████████████ 15

Đang so sánh: vị trí [1] và [2] ← đánh dấu màu
Số bước còn lại: 5
```
**Yêu cầu:** dùng ANSI color codes để tô màu thanh đang so sánh, delay 200ms giữa các bước, cho phép chọn thuật toán.

---
📁 Tham khảo: `Chuong2_TimKiem_SapXep/Chuong2_TimKiem_SapXep.cpp`
