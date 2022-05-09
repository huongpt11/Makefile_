# MAKEFILE 

 Makefile là một file dạng script chứa các thông tin:
+    Cấu trúc project (file, sự phụ thuộc)
+   Các lệnh để tạo file
+   Lệnh make sẽ đọc nội dung Makefile, hiểu kiến trúc của project và thực thi các lệnh.
Ví dụ : khi một phần phụ thuộc nào của một tệp thay đổi thì tệp sẽ được biên dịch lại:
![](https://makefiletutorial.com/assets/dependency_graph.png)

## Cú pháp
![](https://hocarm.org/content/images/2020/04/makefilerule-e1489805882799.png)

Trong đó:
+ **Target**: là file đích, nghĩa là file được hình thành sau khi quá trình make được thực hiện.
+ **Action**: là câu lệnh thực thi để tạo ra Target từ Dependency. Action được thụt lùi vào 1 Tab (phím tab trên bàn phím) so với Target
+ **Rule**: các rule cần thực hiện khi compile
+ **Dependency**: là các file cần thiết để tạo ra target.
## Biến
- Chỉ có thể là chuỗi.
- Thông thường, bạn có thể sử dụng := để khái báo biến , nhưng = cũng hoạt động.
- Các biến tham chiếu sử dụng cả ${} hoặc $().

## Mục tiêu 
- **all** target 
 Để tạo nhiều mục tiêu và muốn tất cả đều chạy .
 - **multiple targets**
Khi có nhiều mục tiêu cho một quy tắc (rule), sử dụng $@ là một biến tự động có chứa tên đích.

## Biến tự động và kí tự đặc biệt
 Kí tự đặc biệt - Wildcard:  * và % đều là kí tự đặc biệt trong Make.

### * Wildcard 
- Tìm kiếm hệ thống tệp của bạn để tìm các tên tệp phù hợp
- Được sử dụng trong mục tiêu, điều kiện tiên quyết hoặc trong hàm kí tự đặc biệt.
### % Wildcard
- Khi được sử dụng ở chế độ "đối sánh", nó khớp với một hoặc nhiều ký tự trong một chuỗi.
- Khi được sử dụng ở chế độ "thay thế", nó sẽ lấy phần gốc được so khớp và thay thế phần đó trong một chuỗi
- % thường được sử dụng nhất trong các định nghĩa quy tắc và trong một số chức năng cụ thể.

**Biến tự động** 
https://www.gnu.org/software/make/manual/html_node/Automatic-Variables.html 
## Fancy Rules
### Quy tắc ngầm 
Một vài biến quan trọng sử dụng quy tắc ngầm: 
+ CC: Chương trình biên dịch chương trình C; mặc định **cc**
+  CXX: Chương trình biên dịch chương trình C ++;mặc định **g ++**
+ CFLAGS: Cờ bổ sung để cung cấp cho trình biên dịch C.
+ CXXFLAGS: Cờ bổ sung để cung cấp cho trình biên dịch C ++
+ CPPFLAGS: Cờ bổ sung để cung cấp cho bộ tiền xử lý C
+ LDFLAGS: Các cờ bổ sung để cung cấp cho trình biên dịch khi chúng được cho là gọi trình liên kết
### Quy tắc mẫu tính
Cú pháp:
**targets...: target-pattern: prereq-patterns ... 
                    commands**

+ Bản chất là mục tiêu (target) đã cho được khớp với mẫu đích(target- pattern)  thông qua ký tự đại diện%
+ Bất cứ thứ gì được kết hợp được gọi là **stem**. Sau đó, **stem** sẽ được thay thế thành **prereq-pattern** để tạo ra các yêu cầu tiên quyết của mục tiêu.
