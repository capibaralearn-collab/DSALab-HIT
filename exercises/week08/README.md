# Tuần 8: Stack & Ứng Dụng — Bài tập

## 🎯 Mục tiêu tuần này
Cài đặt Stack bằng mảng và Linked List. Ứng dụng Stack trong bài toán thực tế.

---

### Bài 1: Cài đặt Stack ⭐⭐
Cài đặt Stack bằng mảng (array-based) và bằng Linked List. So sánh ưu nhược điểm.
//mang
#include <iostream>
#define MAX 1000 // Kích thước tối đa của Stack

class StackArray {
private:
    int top;
    int a[MAX]; // Mảng lưu phần tử

public:
    StackArray() { top = -1; } // Khởi tạo Stack rỗng

    bool push(int x) {
        if (top >= (MAX - 1)) {
            std::cout << "Stack Overflow (Tràn bộ nhớ)!\n";
            return false;
        }
        a[++top] = x;
        return true;
    }

    int pop() {
        if (top < 0) {
            std::cout << "Stack Underflow (Stack rỗng)!\n";
            return 0;
        }
        return a[top--];
    }

    int peek() {
        if (top < 0) {
            std::cout << "Stack rỗng!\n";
            return 0;
        }
        return a[top];
    }

    bool isEmpty() {
        return (top < 0);
    }
};

int main() {
    StackArray s;
    s.push(10);
    s.push(20);
    s.push(30);
    std::cout << "Phan tu top: " << s.peek() << "\n";
    std::cout << "Lay ra: " << s.pop() << "\n";
    std::cout << "Phan tu top sau khi pop: " << s.peek() << "\n";
    return 0;
}

//dslk
#include <iostream>

struct Node {
    int data;
    Node* next;
};

class StackLinkedList {
private:
    Node* top;

public:
    StackLinkedList() { top = nullptr; }

    void push(int x) {
        Node* temp = new Node();
        if (!temp) {
            std::cout << "Heap Overflow (Hết bộ nhớ hệ thống)!\n";
            return;
        }
        temp->data = x;
        temp->next = top; // Trỏ Node mới vào Node top cũ
        top = temp;       // Cập nhật top mới
    }

    int pop() {
        if (isEmpty()) {
            std::cout << "Stack Underflow!\n";
            return 0;
        }
        Node* temp = top;
        int poppedData = temp->data;
        top = top->next; // Dịch chuyển top xuống Node tiếp theo
        delete temp;     // Giải phóng bộ nhớ
        return poppedData;
    }

    int peek() {
        if (!isEmpty()) {
            return top->data;
        }
        std::cout << "Stack rỗng!\n";
        return 0;
    }

    bool isEmpty() {
        return top == nullptr;
    }
    
    // Hàm hủy để tránh rò rỉ bộ nhớ khi hủy đối tượng
    ~StackLinkedList() {
        while (!isEmpty()) {
            pop();
        }
    }
};

int main() {
    StackLinkedList s;
    s.push(10);
    s.push(20);
    s.push(30);
    std::cout << "Phan tu top: " << s.peek() << "\n";
    std::cout << "Lay ra: " << s.pop() << "\n";
    std::cout << "Phan tu top sau khi pop: " << s.peek() << "\n";
    return 0;
}

### Bài 2: Kiểm tra ngoặc hợp lệ ⭐⭐
Kiểm tra chuỗi có đóng mở ngoặc `()`, `[]`, `{}` hợp lệ không. Xử lý cả chuỗi code thực tế.

### Bài 3: Chuyển đổi biểu thức ⭐⭐⭐
Chuyển biểu thức Infix → Postfix → Prefix. In từng bước.

### Bài 4: 🔥 Dự Án Mini — Máy Tính Biểu Thức ⭐⭐⭐
> **Cảm hứng:** [Pilha_Expressão_A — DanielSantDev/Projects-with-Cpp](https://github.com/DanielSantDev/Projects-with-Cpp)

Xây dựng máy tính tính biểu thức toán học bằng Stack:
```
=== 🧮 MÁY TÍNH BIỂU THỨC ===
Nhập biểu thức: (3 + 4) * 2 - 8 / 4

Bước 1 — Chuyển sang Postfix: 3 4 + 2 * 8 4 / -
Bước 2 — Tính toán:
  Push 3 → Stack: [3]
  Push 4 → Stack: [3, 4]
  '+' → Pop 4, Pop 3 → Push 7 → Stack: [7]
  Push 2 → Stack: [7, 2]
  '*' → Pop 2, Pop 7 → Push 14 → Stack: [14]
  ...

✅ Kết quả: (3 + 4) * 2 - 8 / 4 = 12
```
**Yêu cầu:** hỗ trợ +, -, *, /, ^, ngoặc đơn, số thập phân, hiển thị từng bước stack.

---
📁 Tham khảo: `Chuong3_DanhSachLienKet/Chuong3_DanhSachLienKet.cpp`
