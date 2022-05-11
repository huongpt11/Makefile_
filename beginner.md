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
+ ### Bộ lọc và quy tắc mẫu tính
Được dùng để khớp các tệp chính xác
### Quy tắc mẫu
+ Cách để xác định các quy tắc ngầm của riêng bạn.
+ Dạng đơn giản hơn của quy tắc mẫu tĩnh
### Quy tắc dấu hai chấm
Cho phép nhiều quy tắc được xác định cho cùng một mục tiêu.Nếu đây là dấu hai chấm đơn lẻ, một cảnh báo sẽ được in và chỉ bộ lệnh thứ hai sẽ chạy
## Lệnh và thực thi
### Câu lệnh Echoing/Silencing
Thêm ký hiệu @ trước lệnh để ngăn câu lệnh được in mà chỉ in ra kết quả.

Bạn cũng có thể chạy make with -s để thêm @ trước mỗi dòng
### Xử lí lỗi với -k, -i và -
+ Thêm -k khi chạy **make** để tiếp tục chạy ngay cả khi gặp lỗi.
+ Thêm dấu - trước lệnh để loại bỏ lỗi
+ Thêm -i để thực hiện điều này xảy ra cho mọi lệnh.

-> Nếu bạn thực hiện ctrl + C , nó sẽ xóa các mục tiêu mới hơn mà nó vừa thực hiện.
### Đệ quy của make
Để gọi đệ quy một makefile, hãy sử dụng $ (MAKE) thay vì make
-> Sử dụng **export** để thực hiện đệ quy

## Các biến Pt.2
### Flavors và sửa đổi
Có 2 biến Flavors :
+ Đệ quy (sử dụng =)  chỉ tìm kiếm các biến khi lệnh được sử dụng, cho phép bạn thêm vào một biến.
+ Mở rộng đơn giản (sử dụng: =)   giống như lập trình mệnh lệnh thông thường , chỉ những người được xác định mới được mở rộng.
+ ? = chỉ đặt các biến nếu chúng chưa được đặt
+ Khoảng trắng ở cuối dòng không bị xóa, nhưng ở đầu thì có. Để tạo một biến có một khoảng trắng, hãy sử dụng $ (nullstring).
+ Use `+=` để thêm vào
+ 
### Đối số dòng lệnh và ghi đè
 Bạn có thể ghi đè các biến đến từ dòng lệnh bằng cách sử dụng ghi đè. Ở đây chúng tôi đã chạy make với make option_one = hi.

###  Các biến mục tiêu và mẫu cụ thể
 + Các biến có thể được chỉ định cho các mục tiêu cụ thể
 + Bạn có thể chỉ định các biến cho các mẫu mục tiêu cụ thể
 + 
## Điều kiện của Makefile
### Câu điều kiện If/Else
### $(makeflags)



## Function
### First Function
- Chủ yếu được dùng để xử lí văn bản.
- **Cú pháp :**
            1 .`$(fn, arguments)`
         `2.${fn, arguments}`
- Nếu bạn muốn thay thế dấu cách hoặc dấu phẩy, hãy sử dụng các biến

### Thay thế chuỗi
 **Cú pháp: **
         $(patsubst %.pattern,%.replacement,text)
**Cách thay thế:**
           $(text:%.pattern=%.replacement)
 **Thay thế hậu tố:**
         $(text:suffix=replacement)
         -> Không sử dung kí tự % ở đây
### Hàm foreach
**Cú pháp:**
$(foreach var,list,text)
+ Chuyển một danh sách từ sang các từ khác
+ **var** được đặt cho từng từ trong danh sách và **text** được mở rộng cho từng từ
### Hàm If
+ Kiểm tra xem đối số đầu tiên có phải là trống không. Nếu có thì chạy đối số thứ hai, ngược lại thì chạy đối số thứ ba.

### Hàm call
**Cú pháp: **
       $(call variable,param,param)
### Hàm shell
- Thay thế dòng mới bằng dấu cách

## Tính năng khác
### Include Makefiles
- Lệnh include yêu cầu thực hiện đọc một hoặc nhiều tệp Makefiles
### Chỉ thị Vpath
+ Sử dụng vpath để chỉ ra nơi tồn tại một số điều kiện tiên quyết
**Cú pháp: **
vpath <pattern> <directories, space/colon separated>
- <pattern> có thể dùng %, cái  mà nối với không hoặc nhiều kí tự.
### Đa dòng (multiline)
- Kí tự "\" cho phép chúng ta sử dụng nhiều dòng khi câu lệnh quá dài.
### .phony
- Ngăn ngừa việc xung đột giữa file cùng tên với mục tiêu phony.
### .delete_on_error
- Công cụ make sẽ ngừng chạy nếu một câu lệnh trả về một trạng thái khác không.
- DELETE_ON_ERROR sẽ xóa mục tiêu của quy tắc nếu quy tắc không thành công.Điều này sẽ xảy ra cho tất cả các mục tiêu, không chỉ mục tiêu trước đây như PHONY.
