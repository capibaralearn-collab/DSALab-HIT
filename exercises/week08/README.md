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

#include <iostream>
#include <stack>
#include <string>

bool isValidParentheses(const std::string& code) {
    std::stack<char> s;

    for (char ch : code) {
        // 1. Nếu là ngoặc mở, push vào stack
        if (ch == '(' || ch == '[' || ch == '{') {
            s.push(ch);
        }
        // 2. Nếu là ngoặc đóng, kiểm tra tính hợp lệ
        else if (ch == ')' || ch == ']' || ch == '}') {
            // Nếu gặp ngoặc đóng mà stack rỗng -> Không hợp lệ
            if (s.empty()) return false;

            char top = s.top();
            // Kiểm tra xem ngoặc đóng có khớp với ngoặc mở ở đỉnh stack không
            if ((ch == ')' && top == '(') ||
                (ch == ']' && top == '[') ||
                (ch == '}' && top == '{')) {
                s.pop(); // Khớp thì xóa ngoặc mở khỏi stack
            } else {
                return false; // Không khớp cặp -> Lỗi
            }
        }
        // Các ký tự khác (a-z, 0-9, +, -, ...) bị bỏ qua
    }

    // Nếu kết thúc chuỗi mà stack rỗng tức là tất cả đều được khớp
    return s.empty();
}

int main() {
    // Test case 1: Chuỗi code thực tế hợp lệ
    std::string code1 = "if (arr[0] == {x, y}) { return (x + y); }";
    std::cout << "Code 1: " << (isValidParentheses(code1) ? "Hop le" : "Khong hop le") << "\n";

    // Test case 2: Thiếu dấu đóng ngoặc nhọn '}'
    std::string code2 = "void func() { int a = (5 + 2); "; 
    std::cout << "Code 2: " << (isValidParentheses(code2) ? "Hop le" : "Khong hop le") << "\n";

    // Test case 3: Sai thứ tự đóng mở ngoặc ([)]
    std::string code3 = "int main() { return arr[(x + y)]; }"; // Hợp lệ
    std::string code4 = "int main() { return arr[(x + y} ];";  // Không hợp lệ (ngoặc đóng '}' sai vị trí)
    std::cout << "Code 3: " << (isValidParentheses(code3) ? "Hop le" : "Khong hop le") << "\n";
    std::cout << "Code 4: " << (isValidParentheses(code4) ? "Hop le" : "Khong hop le") << "\n";

    return 0;
}

### Bài 3: Chuyển đổi biểu thức ⭐⭐⭐
Chuyển biểu thức Infix → Postfix → Prefix. In từng bước.

#include <iostream>
#include <stack>
#include <string>
#include <cctype>
#include <algorithm>

// Hàm trả về độ ưu tiên của toán tử
int precedence(char c) {
    if (c == '^') return 3;
    if (c == '*' || c == '/') return 2;
    if (c == '+' || c == '-') return 1;
    return -1;
}

// Hàm in trạng thái hiện tại của Stack dưới dạng chuỗi
std::string getStackStr(std::stack<char> s) {
    std::string str = "";
    while (!s.empty()) {
        str = s.top() + str;
        s.pop();
    }
    return str.empty() ? "Rong" : str;
}

std::string infixToPostfix(std::string infix) {
    std::stack<char> s;
    std::string postfix = "";

    std::cout << "\n--- QUA TRINH CHUYEN INFIX -> POSTFIX ---\n";
    std::cout << "Ky tu\t| Stack\t\t| Bieu thuc hien tai\n";
    std::cout << "-------------------------------------------\n";

    for (char ch : infix) {
        // Nếu là khoảng trắng thì bỏ qua
        if (isspace(ch)) continue;

        // 1. Nếu là toán hạng
        if (isalnum(ch)) {
            postfix += ch;
        }
        // 2. Nếu là '('
        else if (ch == '(') {
            s.push(ch);
        }
        // 3. Nếu là ')'
        else if (ch == ')') {
            while (!s.empty() && s.top() != '(') {
                postfix += s.top();
                s.pop();
            }
            if (!s.empty()) s.pop(); // Xóa '('
        }
        // 4. Nếu là toán tử
        else {
            while (!s.empty() && precedence(ch) <= precedence(s.top())) {
                postfix += s.top();
                s.pop();
            }
            s.push(ch);
        }
        // In từng bước
        std::cout << ch << "\t| " << getStackStr(s) << "\t\t| " << postfix << "\n";
    }

    // Pop nốt các toán tử còn lại
    while (!s.empty()) {
        postfix += s.top();
        s.pop();
        std::cout << "End\t| " << getStackStr(s) << "\t\t| " << postfix << "\n";
    }

    return postfix;
}



std::string infixToPrefix(std::string infix) {
    std::cout << "\n--- QUA TRINH CHUYEN INFIX -> PREFIX ---\n";
    
    // Bước 1 & 2: Đảo ngược và đổi dấu ngoặc
    std::reverse(infix.begin(), infix.end());
    for (int i = 0; i < infix.length(); i++) {
        if (infix[i] == '(') infix[i] = ')';
        else if (infix[i] == ')') infix[i] = '(';
    }
    std::cout << "Bieu thuc sau khi dao nguoc & doi ngoak: " << infix << "\n\n";

    std::stack<char> s;
    std::string prefix = "";

    std::cout << "Ky tu\t| Stack\t\t| Bieu thuc hien tai\n";
    std::cout << "-------------------------------------------\n";

    for (char ch : infix) {
        if (isspace(ch)) continue;

        if (isalnum(ch)) {
            prefix += ch;
        } else if (ch == '(') {
            s.push(ch);
        } else if (ch == ')') {
            while (!s.empty() && s.top() != '(') {
                prefix += s.top();
                s.pop();
            }
            if (!s.empty()) s.pop();
        } else {
            // Lưu ý: Dấu '<' thay vì '<=' để đảm bảo tính đúng đắn cho Prefix
            while (!s.empty() && precedence(ch) < precedence(s.top())) {
                prefix += s.top();
                s.pop();
            }
            s.push(ch);
        }
        std::cout << ch << "\t| " << getStackStr(s) << "\t\t| " << prefix << "\n";
    }

    while (!s.empty()) {
        prefix += s.top();
        s.pop();
        std::cout << "End\t| " << getStackStr(s) << "\t\t| " << prefix << "\n";
    }

    // Bước 4: Đảo ngược kết quả lần cuối
    std::reverse(prefix.begin(), prefix.end());
    return prefix;
}




int main() {
    std::string infix = "A + B * (C - D) / E";
    std::cout << "Bieu thuc Infix ban dau: " << infix << "\n";

    std::string postfix = infixToPostfix(infix);
    std::cout << "\n=> KET QUA POSTFIX: " << postfix << "\n";
    
    std::string prefix = infixToPrefix(infix);
    std::cout << "\n=> KET QUA PREFIX: " << prefix << "\n";

    return 0;
}
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
