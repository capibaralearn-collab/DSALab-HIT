# Tuần 6: Danh Sách Liên Kết Đơn — Bài tập

## 🎯 Mục tiêu tuần này
Cài đặt Singly Linked List, thành thạo con trỏ, thêm/xóa/duyệt.


---

### Bài 1: Cài đặt Linked List ⭐⭐
Cài đặt đầy đủ: thêm đầu, thêm cuối, xóa đầu, xóa cuối, xóa theo giá trị, tìm kiếm, in danh sách.

#include <iostream>
using namespace std;

// 1. Định nghĩa cấu trúc của một Node
struct Node {
    int data;
    Node* next;
};

// Hàm tạo một Node mới
Node* createNode(int value) {
    Node* newNode = new Node();
    newNode->data = value;
    newNode->next = nullptr;
    return newNode;
}

// 2. Thêm vào đầu danh sách (Insert At Head)
void insertAtHead(Node*& head, int value) {
    Node* newNode = createNode(value);
    newNode->next = head;
    head = newNode;
}

// 3. Thêm vào cuối danh sách (Insert At Tail)
void insertAtTail(Node*& head, int value) {
    Node* newNode = createNode(value);
    if (head == nullptr) {
        head = newNode;
        return;
    }
    Node* temp = head;
    while (temp->next != nullptr) {
        temp = temp->next;
    }
    temp->next = newNode;
}

// 4. Xóa Node đầu tiên (Delete Head)
void deleteHead(Node*& head) {
    if (head == nullptr) {
        cout << "Danh sach rong, khong the xoa!\n";
        return;
    }
    Node* temp = head;
    head = head->next;
    delete temp; // Giải phóng bộ nhớ
}

// 5. Xóa Node cuối cùng (Delete Tail)
void deleteTail(Node*& head) {
    if (head == nullptr) {
        cout << "Danh sach rong, khong the xoa!\n";
        return;
    }
    if (head->next == nullptr) {
        delete head;
        head = nullptr;
        return;
    }
    Node* temp = head;
    // Duyệt đến Node kế cuối
    while (temp->next->next != nullptr) {
        temp = temp->next;
    }
    delete temp->next; // Xóa Node cuối
    temp->next = nullptr;
}

// 6. Xóa Node theo giá trị (Delete By Value) - Xóa Node đầu tiên tìm thấy
void deleteByValue(Node*& head, int value) {
    if (head == nullptr) {
        cout << "Danh sach rong!\n";
        return;
    }
    // Nếu Node cần xóa nằm ở đầu
    if (head->data == value) {
        deleteHead(head);
        return;
    }

    Node* temp = head;
    // Tìm Node phía trước Node có giá trị cần xóa
    while (temp->next != nullptr && temp->next->data != value) {
        temp = temp->next;
    }

    // Nếu tìm thấy giá trị
    if (temp->next != nullptr) {
        Node* nodeToDelete = temp->next;
        temp->next = temp->next->next;
        delete nodeToDelete;
    }
    else {
        cout << "Khong tim thay gia tri " << value << " de xoa.\n";
    }
}

// 7. Tìm kiếm một giá trị (Search)
bool search(Node* head, int value) {
    Node* temp = head;
    while (temp != nullptr) {
        if (temp->data == value) return true;
        temp = temp->next;
    }
    return false;
}

// 8. In danh sách (Print List)
void printList(Node* head) {
    if (head == nullptr) {
        cout << "Danh sach rong.\n";
        return;
    }
    Node* temp = head;
    while (temp != nullptr) {
        cout << temp->data << " -> ";
        temp = temp->next;
    }
    cout << "NULL\n";
}

// Hàm main để chạy thử nghiệm các chức năng
int main() {
    Node* head = nullptr; // Khởi tạo danh sách rỗng

    cout << "--- Them phan tu ---\n";
    insertAtTail(head, 10);
    insertAtTail(head, 20);
    insertAtTail(head, 30);
    insertAtHead(head, 5);
    printList(head); // Kết quả mong đợi: 5 -> 10 -> 20 -> 30 -> NULL

    cout << "\n--- Tim kiem ---\n";
    cout << "Tim 20: " << (search(head, 20) ? "Thay" : "Khong thay") << endl;
    cout << "Tim 100: " << (search(head, 100) ? "Thay" : "Khong thay") << endl;

    cout << "\n--- Xoa dau, xoa cuoi ---\n";
    deleteHead(head);
    cout << "Sau khi xoa dau: ";
    printList(head); // Kết quả: 10 -> 20 -> 30 -> NULL

    deleteTail(head);
    cout << "Sau khi xoa cuoi: ";
    printList(head); // Kết quả: 10 -> 20 -> NULL

    cout << "\n--- Xoa theo gia tri ---\n";
    insertAtTail(head, 40);
    insertAtTail(head, 50);
    cout << "Danh sach hien tai: ";
    printList(head); // Kết quả: 10 -> 20 -> 40 -> 50 -> NULL

    deleteByValue(head, 40);
    cout << "Sau khi xoa gia tri 40: ";
    printList(head); // Kết quả: 10 -> 20 -> 50 -> NULL

    return 0;
}

### Bài 2: Đảo ngược danh sách ⭐⭐
Đảo ngược Linked List bằng 2 cách: iterative (3 con trỏ) và recursive. So sánh.

### Bài 3: Phát hiện vòng lặp ⭐⭐⭐
Cài đặt Floyd's Cycle Detection (slow/fast pointer). Tìm điểm bắt đầu vòng lặp.

### Bài 4: 🔥 Dự Án Mini — Lịch Sử Trình Duyệt ⭐⭐⭐
> **Cảm hứng:** BaiTapTongHop — Lịch sử trình duyệt (DSALab)

Mô phỏng lịch sử duyệt web bằng Singly Linked List:
```
=== TRÌNH DUYỆT WEB (Linked List) ===
> visit google.com
> visit facebook.com  
> visit youtube.com
> back
← Quay lại: facebook.com
> back
← Quay lại: google.com
> forward
→ Tiến tới: facebook.com
> history
📋 Lịch sử: google.com → facebook.com → youtube.com
                                ↑ (đang ở đây)
```
**Yêu cầu:** hỗ trợ visit, back, forward, history, clear, tối đa 50 trang trong lịch sử.

---
📁 Tham khảo: `Chuong3_DanhSachLienKet/Chuong3_DanhSachLienKet.cpp`
