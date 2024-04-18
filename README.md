<details>
<summary><h1>▶ ⭐C</h1></summary>
<details>
<summary>Variable</summary>

# Biến cục bộ
là biết được lưu ở bộ nhớ stack giá trị biến không đổi khi ra khỏi hàm
nếu dùng static thì nó trở thành biến toàn cục giá trị của biến sẽ bị thay đổi khi ra khỏi hàm
# Biến toàn cục
là biến được khai báo ngoài hàm có giá trị bị thay đổi sau khi ra khỏi hàm vầ tồn tại đến hết chương trình được lưu vào vùng nhớ heap.
# Static cục bộ
lưu vào vùng nhớ heap ứng dụng là khởi tạo giá trị ban đầu không cần khởi tạo lại nhiều lần
# Static toàn cục
chỉ tồn tại trong file chứa nó không thể lấy ra bên ngoài được
# extern
nếu chương trình có nhiều file mà chúng ta không biết biết đó nằm ở file nào thì có thể dùng extern để khai báo trong file chương trình đang viết
có thể sử dụng extern để gọi hàm từ một file khác
# thanh ghi
biến được lưu ở thanh ghi giúp chương trình chạy nhanh hơn khi không cần phải lưu trên ram trước tuy nhiên bộ nhớ thanh ghi có giới hạn
# volatile
để biến không bị tối ưu khi chương trình chạy lặp đi lặp lại nhiều lần
</details>

<details>
<summary> Pointer</summary>

# Con trỏ
là biến lưu địa chỉ
cú pháp khai báo con trỏ:
```int *ptr ```
ví dụ:

```C
#include <stdio.h>
int main(int argc, char const *argv[]){
int a = 20;
int *ptr =&a;
printf("dia chi cua a  %p\n",&a);
printf("gia tri cua a %d\n",*ptr);
return 0;
}
```
# Các loại con trỏ

- **Con trỏ NULL** là con trỏ có địa chỉ là 0x00000000 và giá trị tại địa chỉ đó là 0 và con trỏ không chỉ vào đâu cả.
ví dụ:
```C
int *ptr1; // con trỏ được khởi tạo nhưng nhận một địa chỉ bất kì
int *ptr2= &a; // con trỏ được khởi tạo và nhận địa chỉ của a;
int *ptr3= NULL; // con trỏ NULL không trỏ đến vùng nhớ nào
int *ptr4 = null; // lỗi viết hoa
```
- **Con trỏ hàm (Function Pointers)** là con trỏ chứa địa chỉ của một hàm, dùng để lưu trữ và gọi hàm thông qua con trỏ
```C
Void tong(int a, int b){
    printf("tong cua %d va %d la %d\n",a,b, a+b);
}
Void hieu(int a, int b){
    printf("hieu cua %d va %d la %d\n",a,b, a-b);
}
int main(){
    void (*ptr)(int a, int b);
    ptr = &tong;
    ptr(7,8);
    return 0;
}
```
- **Con trỏ đến con trỏ (pointer to pointer)** là con trỏ chứa địa chỉ của một con trỏ khác
```C
int a = 10;
int *ptr = &a;
int **ptr1=&ptr;
printf("gia tri cua a %d",*ptr); //gia tri cua a 10
printf("dia chi cua a %p",ptr); //dia chi cua a là 00000006679ffa44
printf("gia tri cua ptr %d", **ptr1);//gia tri cua ptr 10
printf("dia chi cua ptr %p",ptr1); //dia chi cua ptr là 00000006679ffa38
```
- **Con trỏ hằng** là con trỏ mà giá trị nó trỏ tới không thể thay đổi được nhưng có thể thay thế địa chỉ mà nó trỏ tới.
```C
int num =10;
const int *ptr= num;
```
- **Con trỏ Void** là con trỏ có thể trỏ tới bất kỳ kiểu dữ liệu nào nhưng phải ép kiểu dữ liệu khi xuất dữ liệu ra
```C
int num = 10;
float pi=3.14;
char C = 'a';
void *ptr;
ptr = &num;
ptr = &pi;
ptr = &C;
printf("gia tri cua num la %d\n",(int *)ptr);
printf("gia tri cua num la %f\n",(float *)ptr);
printf("gia tri cua num la %c\n",(char *)ptr);
```
- **Con trỏ vào hàm** là con trỏ lưu địa chỉ của một hàm
ví dụ:
```C
int tong(int a, int b){
    return a+b;
}
int hieu(int a, int b){
    return a-b;
}
void pheptinh(int a, int b, int (*ptr)(int , int)){
    int ketqua = tinh(a,b);
    printf("ket qua = %d\n",ketqua);
}
int main(){
    int a=1 , b=2;
    pheptinh(a,b,tong);
    pheptinh(a,b,hieu);
}
```
- **Con trỏ hàm parameters** là con trỏ truyền một tham số cho hàm khác.
ví dụ:
```C
void greet(){
    printf("hello world!\n");
}
void performAction(void(*ptr)()){
    ptr();
}
int main(){
    performAction(greet);
    return 0;
}
```
 ***Những lưu ý khi sử dụng con trỏ***
- khi khởi tạo con trỏ NULL phải viết hoa chữ NULL
- không nên sử dụng con trỏ khi chưa khởi tạo: kết quả tính toán có thể sẽ phát sinh lỗi không lường trước được nếu chưa khởi tạo con trỏ.
- sử dụng biến con trỏ sai cách.
*** Tác dụng của con trỏ***
- Thay đổi giá trị tại vùng mà con trỏ trỏ đến
ví dụ:
```C
int a= 10; // gán giá trị a =10
int *ptr = &a; // con trỏ ptr trỏ đến địa chỉ của a
*ptr =20; //giá trị tại địa chỉ của a bằng 20
```