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

void reverseIterative(Node*& head) {
    Node* prev = nullptr;
    Node* curr = head;
    Node* next = nullptr;
    
    while (curr != nullptr) {
        next = curr->next; // 1. Giữ lại địa chỉ của Node tiếp theo
        curr->next = prev; // 2. Đảo ngược hướng con trỏ của Node hiện tại
        
        // 3. Dịch chuyển hai con trỏ prev và curr lên một bước
        prev = curr;
        curr = next;
    }
    // Sau khi kết thúc, prev sẽ là Node cuối cũ (tức là Node đầu mới)
    head = prev;
}

de quy 

Node* reverseRecursiveHelper(Node* head) {
    // Điều kiện dừng: nếu danh sách rỗng hoặc chỉ có 1 phần tử
    if (head == nullptr || head->next == nullptr) {
        return head;
    }
    
    // Đệ quy đảo ngược danh sách phía sau
    Node* newHead = reverseRecursiveHelper(head->next);
    
    // Bẻ ngược con trỏ: Node kế tiếp sẽ trỏ lại chính Node hiện tại
    head->next->next = head;
    
    // Ngắt kết nối cũ để tránh bị vòng lặp vô hạn (Cycle)
    head->next = nullptr;
    
    return newHead;
}

// Hàm wrapper để cập nhật lại head của danh sách
void reverseRecursive(Node*& head) {
    head = reverseRecursiveHelper(head);
}



### Bài 3: Phát hiện vòng lặp ⭐⭐⭐
Cài đặt Floyd's Cycle Detection (slow/fast pointer). Tìm điểm bắt đầu vòng lặp.

#include <iostream>

using namespace std;

// Định nghĩa cấu trúc của một Node trong Linked List
struct Node {
    int data;
    Node* next;
    
    Node(int val) {
        data = val;
        next = nullptr;
    }
};

// Hàm phát hiện và tìm điểm bắt đầu của vòng lặp
Node* detectCycleStart(Node* head) {
    if (head == nullptr || head->next == nullptr) {
        return nullptr; // Không thể có vòng lặp nếu danh sách rỗng hoặc chỉ có 1 phần tử
    }

    Node* slow = head;
    Node* fast = head;

    // Giai đoạn 1: Phát hiện xem có vòng lặp hay không
    bool hasCycle = false;
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;          // Rùa đi 1 bước
        fast = fast->next->next;    // Thỏ đi 2 bước

        if (slow == fast) {         // Rùa và Thỏ gặp nhau
            hasCycle = true;
            break;
        }
    }

    // Nếu không có vòng lặp, trả về nullptr
    if (!hasCycle) {
        return nullptr;
    }

    // Giai đoạn 2: Tìm điểm bắt đầu của vòng lặp
    fast = head; // Đưa Thỏ về lại đầu danh sách
    while (slow != fast) {
        slow = slow->next; // Lúc này cả hai đều đi 1 bước
        fast = fast->next;
    }

    return slow; // Hoặc trả về fast, vì lúc này slow == fast (điểm bắt đầu vòng lặp)
}

// Hàm tiện ích để in kết quả kiểm tra
void checkAndPrintResult(Node* head) {
    Node* cycleStart = detectCycleStart(head);
    if (cycleStart != nullptr) {
        cout << "-> Danh sach co vong lap! Bat dau tai Node co gia tri: " << cycleStart->data << endl;
    } else {
        cout << "-> Danh sach khong co vong lap." << endl;
    }
}

int main() {
    // Tạo các Node độc lập
    Node* head = new Node(1);
    Node* node2 = new Node(2);
    Node* node3 = new Node(3);
    Node* node4 = new Node(4);
    Node* node5 = new Node(5);

    // Nối các Node thành danh sách: 1 -> 2 -> 3 -> 4 -> 5
    head->next = node2;
    node2->next = node3;
    node3->next = node4;
    node4->next = node5;

    // Trường hợp 1: Chưa tạo vòng lặp
    cout << "Test 1: ";
    checkAndPrintResult(head);

    // Trường hợp 2: Tạo vòng lặp (Cho Node 5 trỏ ngược về Node 3)
    // Danh sách sẽ thành: 1 -> 2 -> 3 -> 4 -> 5 -> (quay lại 3)
    node5->next = node3;
    
    cout << "Test 2: ";
    checkAndPrintResult(head);

    // Giải phóng bộ nhớ (Lưu ý: Với danh sách có vòng lặp, việc giải phóng 
    // cần cẩn thận để tránh vòng lặp vô hạn, ở đây ta bẻ vòng lặp trước khi xóa)
    node5->next = nullptr;
    delete head; delete node2; delete node3; delete node4; delete node5;

    return 0;
}

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
