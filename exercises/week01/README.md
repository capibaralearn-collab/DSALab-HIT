# Tuần 1: Tổng Quan C++ & Big-O — Bài tập

## 🎯 Mục tiêu tuần này
Hiểu Big-O, phân tích độ phức tạp, ôn tập C++ cơ bản.

---
2125110152 nguyễn trí công
### Bài 1: Phân tích Big-O ⭐
Xác định Big-O của 10 đoạn code C++ cho trước. Giải thích tại sao.
int getElement(int arr[], int i) {
    return arr[i]; // truy cập trực tiếp
}
//Tại sao O(1)? Truy cập phần tử mảng theo chỉ số là phép tính địa chỉ bộ nhớ trực tiếp: địa_chỉ = base + i × sizeof(int). Không có vòng lặp, không phụ thuộc vào kích thước mảng n. Số bước thực hiện luôn là hằng số.

int binarySearch(int arr[], int n, int target) {
    int lo = 0, hi = n - 1;
    while (lo <= hi) {
        int mid = (lo + hi) / 2;
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) lo = mid + 1;
        else hi = mid - 1;
    }
    return -1;
}
//Tại sao O(log n)? Mỗi lần lặp, không gian tìm kiếm bị chia đôi. Với n = 1.000.000 phần tử, chỉ cần tối đa ~20 bước (log₂ 1.000.000 ≈ 20). Số lần lặp = log₂(n).

int findMax(int arr[], int n) {
    int maxVal = arr[0];
    for (int i = 1; i < n; i++) {  // duyệt 1 lần
        if (arr[i] > maxVal)
            maxVal = arr[i];
    }
    return maxVal;
}
//Tại sao O(n)? Vòng lặp duyệt qua mỗi phần tử đúng một lần. Số phép so sánh = n − 1. Khi n tăng gấp đôi, thời gian chạy cũng tăng gấp đôi — tỉ lệ tuyến tính.

void printPairs(int arr[], int n) {
    for (int i = 0; i < n; i++)        // n lần
        for (int j = 0; j < n; j++)    // n lần
            cout << arr[i] << "," << arr[j] << "
";
}
//Tại sao O(n²)? Vòng lặp ngoài chạy n lần, vòng lặp trong cũng chạy n lần → tổng số lần thực thi phần thân = n × n = n². Đây là dấu hiệu điển hình của 2 vòng lặp lồng nhau duyệt cùng tập dữ liệu.

void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++)
        for (int j = 0; j < n - i - 1; j++)
            if (arr[j] > arr[j+1])
                swap(arr[j], arr[j+1]);
}
//Tại sao O(n²)? Tổng số lần so sánh = (n−1) + (n−2) + … + 1 = n(n−1)/2. Bỏ hệ số và hằng số, ta còn O(n²). Dù vòng trong ngắn dần, bậc tăng trưởng vẫn là bậc hai.

void mergeSort(int arr[], int l, int r) {
    if (l >= r) return;
    int mid = (l + r) / 2;
    mergeSort(arr, l, mid);    // chia đôi: log n tầng
    mergeSort(arr, mid+1, r);
    merge(arr, l, mid, r);     // merge: O(n) mỗi tầng
}
//Tại sao O(n log n)? Cây đệ quy có log n tầng (mỗi tầng chia đôi mảng). Tại mỗi tầng, hàm merge() xử lý tổng cộng n phần tử. Tổng = n × log n.

int fib(int n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);  // 2 nhánh đệ quy
}
//Tại sao O(2ⁿ)? Mỗi lời gọi sinh ra 2 lời gọi con. Cây đệ quy có độ sâu n và gần như đầy đủ → tổng số node ≈ 2ⁿ. Đây là độ phức tạp cực kỳ tệ — fib(50) cần ~1.000 tỷ phép tính!

bool isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i * i <= n; i++)  // chỉ đến √n
        if (n % i == 0) return false;
    return true;
}
//Tại sao O(√n)? Nếu n có ước số d > √n thì n/d < √n đã được kiểm tra rồi — không cần kiểm tra tiếp. Do đó vòng lặp chỉ chạy đến √n, tức khoảng √n lần lặp.

bool hasCommon(int A[], int a, int B[], int b) {
    for (int i = 0; i < a; i++)    // a lần
        for (int j = 0; j < b; j++)  // b lần
            if (A[i] == B[j]) return true;
    return false;
}
//Tại sao O(a × b) chứ không phải O(n²)? Hai mảng có kích thước khác nhau (a và b). Không thể gộp làm một biến n. Nếu a ≈ b thì O(a×b) ≈ O(n²), nhưng phải giữ nguyên hai biến để chính xác.

int countBits(int n) {
    int count = 0;
    while (n) {
        n = n & (n - 1);  // xóa bit 1 thấp nhất
        count++;
    }
    return count;
}
//Tại sao O(log n)? Số n có tối đa ⌊log₂ n⌋ + 1 bit nhị phân. Mỗi lần lặp, phép n & (n−1) xóa đúng một bit 1 → số lần lặp = số bit 1 ≤ tổng số bit = O(log n).

### Bài 2: Đo thời gian thực tế ⭐⭐
Dùng `chrono` đo thời gian chạy của O(n), O(n²), O(log n) với n = 1.000 → 100.000. In bảng kết quả.

#include <chrono>
using namespace std::chrono;

auto t0 = high_resolution_clock::now();
// ... code cần đo ...
auto t1 = high_resolution_clock::now();

auto elapsed = duration_cast<microseconds>(t1 - t0).count();

### Bài 3: Tối ưu hàm ⭐⭐
Cho 3 hàm O(n²) — tối ưu xuống O(n) hoặc O(n log n). Chứng minh bằng cách đo thời gian.

### Bài 4: 🔥 Dự Án Mini — Big-O Benchmark Tool ⭐⭐⭐
> **Cảm hứng:** [algorithm-visualizer.org](https://algorithm-visualizer.org)

Viết chương trình **BenchmarkTool** hiển thị bảng so sánh tốc độ các thuật toán:
```
╔══════════════╦══════════╦══════════╦══════════╗
║   Thuật toán ║  n=1000  ║  n=10000 ║ n=100000 ║
╠══════════════╬══════════╬══════════╬══════════╣
║    O(1)      ║  0.001ms ║  0.001ms ║  0.001ms ║
║    O(log n)  ║  0.003ms ║  0.004ms ║  0.005ms ║
║    O(n)      ║  0.12ms  ║  1.2ms   ║  12ms    ║
║    O(n²)     ║  8ms     ║  800ms   ║  80000ms ║
╚══════════════╩══════════╩══════════╩══════════╝
```

**Yêu cầu:** dùng `std::chrono`, hiển thị bảng căn chỉnh đẹp, xuất ra file `benchmark.txt`.

---
📁 Tham khảo: `Chuong1_TongQuan/Chuong1_TongQuan.cpp`
