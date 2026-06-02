Bài 1: Mảng cơ bản ⭐
Nhập mảng n phần tử. Tính min, max, trung bình, tổng. Không dùng STL.
#include <iostream>
using namespace std;
const int MAX = 100;

void nhapMang(int a[], int n) {
    for (int i = 0; i < n; i++) {
        cout << "a[" << i << "] = ";
        cin >> a[i];
    }
}

int timMin(int a[], int n) {
    int min = a[0];
    for (int i = 1; i < n; i++) {
        if (a[i] < min)
            min = a[i];
    }
    return min;
}

int timMax(int a[], int n) {
    int max = a[0];
    for (int i = 1; i < n; i++) {
        if (a[i] > max)
            max = a[i];
    }
    return max;
}

int tinhTong(int a[], int n) {
    int s = 0;
    for (int i = 0; i < n; i++)
        s += a[i];
    return s;
}

float tinhTrungBinh(int a[], int n) {
    return (float)tinhTong(a, n) / n;
}

int main() {
    int a[MAX];
    int n;
    /*ct vo vong lap do while de ktr neu n lon hon 0 thoat vong lap*/
    do {
        cout << "Nhap n: ";
        cin >> n;
    } while (n <= 0);
    /* goi ham void nhapmang sau do chay vong lap de nguoi dung nhap va thoat vong lap sau khi dk vong for sai  */
    nhapMang(a, n);
    /* goi ham timMin khoi tao min la ptu dau tien cua mang sau do duyet tu ptu thu hai den het mang neu ptu nao nho hon min thi cap nhat bien min sau khi duyet xong tra ve min */
    cout << "Min     : " << timMin(a, n) << endl;
    /* goi ham timMax khoi tao max la ptu dau tien cua mang sau do duyet tu ptu thu hai den het mang neu ptu nao lon hon max thi cap nhat bien max sau khi duyet xong tra ve max */
    cout << "Max     : " << timMax(a, n) << endl;
    /*goi ham tinhtong khoi tao s = 0 sau do chay vong lap for tu phan tu dau tien den het mang , moi lan lap thi cong don phan tu hien tai vao s sau khi chay xong tra ve s */
    cout << "Tong    : " << tinhTong(a, n) << endl;
    /*goi ham tinhtrungbinh trong ham tinh trung binh goi tiep ham tinh tong sau khi duoc tong dem  chia cho n va phai ep kieu sang float */
    cout << "Trung binh: " << tinhTrungBinh(a, n) << endl;

    return 0;
}
/*
1. Bắt đầu chương trình - Hàm main()
Vào vòng do-while:
In ra: Nhap n:
Người dùng nhập: 5 → n = 5
Kiểm tra while (n <= 0) → sai → thoát vòng lặp
Gọi hàm: nhapMang(a, 5)
2. Vào hàm void nhapMang(int a[], int n)
Vòng lặp nhập mảng:
i = 0: In a[0] =  → Người dùng nhập 7 → a[0] = 7
i = 1: In a[1] =  → Người dùng nhập 3 → a[1] = 3
i = 2: In a[2] =  → Người dùng nhập 12 → a[2] = 12
i = 3: In a[3] =  → Người dùng nhập 5 → a[3] = 5
i = 4: In a[4] =  → Người dùng nhập 8 → a[4] = 8
→ Mảng sau khi nhập: [7, 3, 12, 5, 8]
3. Quay lại main() → Gọi timMin(a, 5)
Vào hàm int timMin(int a[], int n):
int min = a[0] = 7
Vòng lặp:
i=1: 3 < 7 → min = 3
i=2: 12 < 3 → sai
i=3: 5 < 3 → sai
i=4: 8 < 3 → sai
→ Trả về 3
4. Gọi timMax(a, 5)
Vào hàm int timMax(int a[], int n):
int max = a[0] = 7
Vòng lặp:
i=1: 3 > 7 → sai
i=2: 12 > 7 → max = 12
i=3: 5 > 12 → sai
i=4: 8 > 12 → sai
→ Trả về 12
5. Gọi tinhTong(a, 5)
Vào hàm int tinhTong(int a[], int n):
int s = 0
Vòng lặp:
i=0: s = 0 + 7 = 7
i=1: s = 7 + 3 = 10
i=2: s = 10 + 12 = 22
i=3: s = 22 + 5 = 27
i=4: s = 27 + 8 = 35
→ Trả về 35
6. Gọi tinhTrungBinh(a, 5)
Vào hàm float tinhTrungBinh(int a[], int n):
Gọi tinhTong(a, 5) → được 35
Tính: (float)35 / 5 = 7.0
→ Trả về 7
7. Quay lại main() - In kết quả
*/
Bài 2: Mảng 2D ⭐⭐
Nhân 2 ma trận n×n. Tính định thức ma trận 3×3. Hiển thị đẹp.
#include <iostream>

using namespace std;

const int MAX = 100;

void nhap_mt(int a[][MAX], int n) {
	
	for (int i = 0; i < n; i++) {
		for (int j = 0;j < n;j++) {
			cin >> a[i][j];
		}
	}
}

void xuat_mt(int a[][MAX], int n) {
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			cout << a[i][j] << ' ';
		}
		cout << endl;
	}
}

void nhan_mt(int a[][MAX], int b[][MAX], int c[][MAX], int n) {
	for (int i = 0; i < n; i++)
		for (int j = 0; j < n; j++) {
			c[i][j] = 0;
			for (int k = 0; k < n; k++)
				c[i][j] += a[i][k] * b[k][j];
		}
}

int main() {
	int n;
	int a[MAX][MAX], b[MAX][MAX], c[MAX][MAX];

	cout << "nhap kich thuoc n cho 2 ma tran n x n: ";
	cin >> n;

	
	cout << "nhap ma tran A : " << endl;
	nhap_mt(a, n);
	

	cout << "nhap ma tran B : "<< endl;
	nhap_mt(b, n);
	
	nhan_mt(a, b, c, n);
	cout << "ma tra A " << endl;
	xuat_mt(a, n);
	cout << "ma tra B " << endl;
	xuat_mt(b, n);
	cout << "nhan hai ma tran " << endl;
	xuat_mt(c, n);
	return 0;
}

Bài 3: Con trỏ & cấp phát động ⭐⭐
Cài đặt mảng động tự resize (như std::vector đơn giản). Hỗ trợ push_back, pop_back, at(i).
#include <iostream>
using namespace std;

struct MyVector {
    int* data;
    int  size, capacity;
};

void init(MyVector& v) {
    v.size = 0; v.capacity = 2;
    v.data = new int[2];
}

void destroy(MyVector& v) {
    delete[] v.data;
    v.data = nullptr; v.size = v.capacity = 0;
}

void resize(MyVector& v) {
    v.capacity *= 2;
    int* t = new int[v.capacity];
    for (int i = 0; i < v.size; i++) t[i] = v.data[i];
    delete[] v.data;
    v.data = t;
    cout << "  [resize -> cap=" << v.capacity << "]\n";
}

void push_back(MyVector& v, int x) {
    if (v.size == v.capacity) resize(v);
    v.data[v.size++] = x;
}

void pop_back(MyVector& v) {
    if (v.size == 0) cout << "  [!] Rong!\n";
    else v.size--;
}

int at(MyVector& v, int i) {
    if (i < 0 || i >= v.size) { cout << "  [!] Out of range!\n"; return -1; }
    return v.data[i];
}

void print(MyVector& v) {
    cout << "  [size=" << v.size << " cap=" << v.capacity << "]: [";
    for (int i = 0; i < v.size; i++) cout << v.data[i] << (i<v.size-1?", ":"");
    cout << "]\n";
}

int main() {
    MyVector v; init(v);

    cout << "\n=== PUSH_BACK ===\n";
    for (int x : {10, 20, 30, 40, 50}) { push_back(v, x); print(v); }

    cout << "\n=== AT ===\n";
    cout << "  at(0)=" << at(v,0) << "  at(2)=" << at(v,2) << "\n";
    at(v, 9); // out of range

    cout << "\n=== POP_BACK ===\n";
    pop_back(v); print(v);
    pop_back(v); print(v);

    destroy(v);
    cout << "\n  [destroy OK]\n";
}

Bài 4: 🔥 Dự Án Mini — Student Score Manager ⭐⭐⭐
Cảm hứng: BaiTapTongHop — Quản lý sinh viên (DSALab)

Xây dựng hệ thống quản lý điểm sinh viên bằng mảng động:

Thêm / xóa / sửa sinh viên (tên, MSSV, điểm)
Sắp xếp theo điểm (dùng Selection Sort hoặc Bubble Sort)
Tìm kiếm theo tên hoặc MSSV (Linear Search)
Thống kê: điểm cao nhất, thấp nhất, trung bình lớp
Xuất danh sách ra file diem_sinhvien.txt
=== QUẢN LÝ ĐIỂM SINH VIÊN ===
1. Thêm sinh viên
2. Xóa sinh viên
3. Tìm kiếm
4. Xếp hạng lớp
5. Xuất báo cáo
0. Thoát

   #include <iostream>
#include <fstream>
#include <iomanip>
#include <cstring>
using namespace std;

struct SV { char mssv[12], ten[50]; float diem; };
struct DS { SV* ds; int size, cap; };

void init(DS& d)    { d.size=0; d.cap=4; d.ds=new SV[4]; }
void destroy(DS& d) { delete[] d.ds; d.ds=nullptr; d.size=d.cap=0; }
void resize(DS& d)  { SV* t=new SV[d.cap*=2]; for(int i=0;i<d.size;i++) t[i]=d.ds[i]; delete[] d.ds; d.ds=t; }

const char* xepLoai(float x) {
    if(x>=9) return "Xuat sac"; if(x>=8) return "Gioi";
    if(x>=6.5) return "Kha";    if(x>=5) return "TB"; return "Yeu";
}

void ke() { cout<<"  +"<<setfill('-')<<setw(13)<<"+"<<setw(32)<<"+"<<setw(8)<<"+"<<setw(12)<<"+"<<setfill(' ')<<"\n"; }

void inDS(DS& d) {
    if(!d.size) { cout<<"  [!] Danh sach trong.\n"; return; }
    ke();
    cout<<"  | "<<left<<setw(10)<<"MSSV"<<" | "<<setw(29)<<"Ho Ten"<<" | "<<setw(5)<<"Diem"<<" | "<<setw(9)<<"Xep loai"<<" |\n";
    ke();
    for(int i=0;i<d.size;i++)
        cout<<"  | "<<left<<setw(10)<<d.ds[i].mssv<<" | "<<setw(29)<<d.ds[i].ten
            <<" | "<<right<<fixed<<setprecision(1)<<setw(5)<<d.ds[i].diem<<" | "<<left<<setw(9)<<xepLoai(d.ds[i].diem)<<" |\n";
    ke(); cout<<"  Tong: "<<d.size<<" SV\n";
}

void them(DS& d) {
    if(d.size==d.cap) resize(d);
    SV& s=d.ds[d.size];
    cout<<"  MSSV: "; cin>>s.mssv; cin.ignore();
    cout<<"  Ten : "; cin.getline(s.ten,50);
    cout<<"  Diem: "; cin>>s.diem;
    if(s.diem<0||s.diem>10) { cout<<"  [!] Diem khong hop le!\n"; return; }
    d.size++; cout<<"  [+] Da them.\n";
}

void xoa(DS& d) {
    char ms[12]; cout<<"  MSSV can xoa: "; cin>>ms;
    for(int i=0;i<d.size;i++) if(!strcmp(d.ds[i].mssv,ms)) {
        for(int j=i;j<d.size-1;j++) d.ds[j]=d.ds[j+1];
        d.size--; cout<<"  [-] Da xoa.\n"; return;
    }
    cout<<"  [!] Khong thay.\n";
}

void sua(DS& d) {
    char ms[12]; cout<<"  MSSV can sua: "; cin>>ms;
    for(int i=0;i<d.size;i++) if(!strcmp(d.ds[i].mssv,ms)) {
        cin.ignore();
        cout<<"  Ten moi : "; cin.getline(d.ds[i].ten,50);
        cout<<"  Diem moi: "; cin>>d.ds[i].diem;
        cout<<"  [*] Da cap nhat.\n"; return;
    }
    cout<<"  [!] Khong thay.\n";
}

void tim(DS& d) {
    int ch; char kw[50];
    cout<<"  (1)MSSV (2)Ten: "; cin>>ch; cin.ignore();
    cout<<"  Tu khoa: "; cin.getline(kw,50);
    ke(); bool found=false;
    for(int i=0;i<d.size;i++) {
        bool ok=(ch==1)?!strcmp(d.ds[i].mssv,kw):strstr(d.ds[i].ten,kw)!=nullptr;
        if(ok) { cout<<"  | "<<left<<setw(10)<<d.ds[i].mssv<<" | "<<setw(29)<<d.ds[i].ten<<" | "<<right<<fixed<<setprecision(1)<<setw(5)<<d.ds[i].diem<<" |\n"; found=true; }
    }
    ke(); if(!found) cout<<"  [!] Khong tim thay.\n";
}

void sapXep(DS& d) {
    for(int i=0;i<d.size-1;i++) { int mx=i;
        for(int j=i+1;j<d.size;j++) if(d.ds[j].diem>d.ds[mx].diem) mx=j;
        if(mx!=i) swap(d.ds[i],d.ds[mx]);
    }
    cout<<"  [OK] Da sap xep.\n"; inDS(d);
}

void thongKe(DS& d) {
    if(!d.size) { cout<<"  [!] Trong.\n"; return; }
    float mn=d.ds[0].diem, mx=d.ds[0].diem, tong=0; int iMn=0,iMx=0;
    for(int i=0;i<d.size;i++) {
        tong+=d.ds[i].diem;
        if(d.ds[i].diem<mn){mn=d.ds[i].diem;iMn=i;}
        if(d.ds[i].diem>mx){mx=d.ds[i].diem;iMx=i;}
    }
    cout<<fixed<<setprecision(2)
        <<"\n  TB      : "<<tong/d.size
        <<"\n  Cao nhat: "<<mx<<" ("<<d.ds[iMx].ten<<")"
        <<"\n  Thap nht: "<<mn<<" ("<<d.ds[iMn].ten<<")\n";
}

void xuatFile(DS& d) {
    ofstream f("diem_sinhvien.txt");
    f<<left<<setw(12)<<"MSSV"<<setw(30)<<"Ho Ten"<<setw(8)<<"Diem"<<"Xep loai\n"<<string(60,'-')<<"\n";
    for(int i=0;i<d.size;i++)
        f<<left<<setw(12)<<d.ds[i].mssv<<setw(30)<<d.ds[i].ten
         <<fixed<<setprecision(1)<<setw(8)<<d.ds[i].diem<<xepLoai(d.ds[i].diem)<<"\n";
    f.close(); cout<<"  [OK] Xuat 'diem_sinhvien.txt'.\n";
}

void menu() {
    cout<<"\n  ╔══════════════════════════════╗\n"
          "  ║  QUAN LY DIEM SINH VIEN     ║\n"
          "  ╠══════════════════════════════╣\n"
          "  ║ 1.Them  2.Xoa   3.Sua       ║\n"
          "  ║ 4.Hien  5.Tim   6.SapXep    ║\n"
          "  ║ 7.ThongKe       8.XuatFile  ║\n"
          "  ║ 0.Thoat                     ║\n"
          "  ╚══════════════════════════════╝\n"
          "  Chon: ";
}

int main() {
    DS d; init(d); int ch;
    do {
        menu(); cin>>ch;
        switch(ch) {
            case 1:them(d);    break; case 2:xoa(d);     break;
            case 3:sua(d);     break; case 4:inDS(d);    break;
            case 5:tim(d);     break; case 6:sapXep(d);  break;
            case 7:thongKe(d); break; case 8:xuatFile(d);break;
            case 0:cout<<"  Tam biet!\n"; break;
            default:cout<<"  [!] Sai lua chon.\n";
        }
    } while(ch!=0);
    destroy(d);
}
