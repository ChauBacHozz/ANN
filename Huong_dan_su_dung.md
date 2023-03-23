# ANN

# Hướng dẫn sử dụng gói ann để chạy model mạng nơ ron nhân tạo cơ bản (ANN)

## Cài đặt python và các ứng dụng cần thiết
- Bước 1: Tải python từ trang: https://www.python.org/downloads/
Chú ý: Tích vào 2 ô Install launcher for all users và Add Python to PATH, sau khi cài đặt mở ứng dụng cmd và gõ "python --version" và ấn Enter, nếu hiển thị phiên bản python đã cài về thì đã cài đặt thành công, nếu không thì ấn lại vào file installer vừa tải về để gỡ cài đặt python. Sau đó bấm lại vào installer để cài lại python, lưu ý hãy chọn vào 2 dòng trên.
- Bước 2: Cài đặt visual studio code  (VS Code) từ trang: https://code.visualstudio.com/download
- Bước 3: sau khi cài đặt VS Code, mở ứng dụng và vào file -> chọn open folder -> Tại một folder mới tại nơi muốn lưu code rời ấn Open
- Bước 4: ở màn hình VS Code, vào phần extenson (Ctrl + Shift + X) gõ "python" (nếu không hiển thị chữ install ở dưới tức là đã được cài đặt, nếu không hãy bấm vào install), sau đó gõ "jupyter" và cài đặt lựa chọn xuất hiện đầu tiên
![image](https://user-images.githubusercontent.com/90232557/226867539-d31397b4-444e-4148-82f1-089b563cc1c6.png)
- Bước 5: trong phần tìm kiếm của extension gõ "Code runner" và cài đặt lựa chọn xuất hiện đầu tiên

## Tạo file thực thi và cài đặt các thư viện cần thiết
- Bước 1: Ấn Ctrl + Shift + E để mở phần Explorer của VS Code, tạo file python để chạy code bằng cách gõ {Tên file}.py, ví dụ: main.py sau đó ấn Enter (Tất cả code python sẽ nằm trong file này)
- Bước 2: Ấn Ctrl + Shift + ` để mở cửa sổ terminal, hoặc vào phần Terminal ở thành toolbar của VS Code -> chọn New Terminal
![image](https://user-images.githubusercontent.com/90232557/226869390-0af1db5d-06d1-46ae-a5a1-d8d0f3ddbecc.png)
- Bước 3: Gõ lệnh "pip install numpy, pandas, matplotlib, scikit-learn, openpyxl" vào cửa sổ terminal rồi ấn Enter, chờ quá trình cài đặt cho đến khi có thông báo "Successfully installed" hiện lên là coi như đã cài đặt thành công
- Bước 4: Vào đường link https://github.com/ChauBacHozz/ANN bấm vào nút Code màu xanh lá, chọn Download ZIP, sau đó giải nén và copy file ANN_pkg trong folder ANN-main vào cùng thư mục với file main.py
![image](https://user-images.githubusercontent.com/90232557/226871446-f4abf4ce-4937-42ce-89ff-912600c33db6.png)

## Sử dụng ANN bằng python
### Giới thiệu các thư viện: numpy, matplotlib, pandas
- numpy: thư việc đại số tuyến tính của python (xử lý nhân ma trận, nghịch đảo ma trận, vv...) dể xử lý số liệu
- matplotlib: thư viện hiển thị dữ liệu (giống như Chart của excel)
- pandas: thư viện dùng để đọc dataset từ các file dạng csv, xlsx, text,...
### Bước 1: Import thư viện vào file code
- Ở đầu file python, nhập vào các dòng sau:
```
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from ANN_pkg import *
```
- Từ **as** có nghĩa là ta định nghĩa tên gọi tắt cho thư viện, nhằm giúp cho việc code không bị dài dòng và thuận tiện cho việc gọi các hàm từ thư viện
- import * có nghĩa là ta import tất cả các hàm cần sử dụng từ gói ANN
### Bước 2: Sử dụng python để đọc file dữ liệu và tiến hành tiền xử lý dữ liệu
##### Đọc file dữ liệu
- Copy file dữ liệu (dạng csv, xlsx, txt, ...) vào cùng thư mục với file python
![image](https://user-images.githubusercontent.com/90232557/227142630-d6602b79-34e7-4b98-be1b-46ead31ac61b.png)
- Sau đó trong file .py, tạo một biến đặt tên là data (data sẽ lưu trữ thông tin của file dữ liệu) và đọc bảng dữ liệu bằng lệnh pd.read_excel({Tên file})
- Xuống dòng gõ lệnh print(data) rồi chuột phải, chọn "Run Code" để kiểm tra python đã đọc được dữ liệu hay chưa
![image](https://user-images.githubusercontent.com/90232557/227144059-26e81450-f8d0-4bde-bd2f-7b0002ef8f55.png)
  *Nếu dữ liệu được đọc thành công, sau khi run code bảng dữ liệu sẽ hiển thị ở trong cửa sổ terminal như hình*
##### Tiền xử lý dữ liệu
- Kiểm tra dữ liệu trống: Kiểm tra file dữ liệu có ô nào bị bỏ trống không bằng lệnh print(data.isnull().values.any()) sau đó run code, nếu cửa sổ terminal hiện lên là False tức là không có ô nào trong bảng dữ liệu bị trống, còn nếu hiện lên là True thì cần rà soát kiểm tra lại file dữ liệu, nếu không khi luyện mạng sẽ gây lỗi
- Co giãn dữ liệu: với bảng dữ liệu nồng độ - tín hiệu của phổ UV-VIS thì dữ liệu khá đơn giản nên không cần tới quá nhiều kĩ thuật tiền xủ lý dữ liệu, tuy nhiên nếu giá trị giữa các cột nồng độ - Abs cách nhau quá lớn (>10 lần), có thể co dữ liệu về các giá trị nằm trong khoảng 0 - 1 để khiến cho tốc độ luyện mạng nhanh hơn
![image](https://user-images.githubusercontent.com/90232557/227148017-9260b617-57bc-4e9a-a051-8d7b7666b2ed.png)
 + *Như ví dụ trên, giá trị các cột nồng độ cao hơn các giá trị Abs gấp 100 lần*
 + Để co giãn dữ liệu, ta thêm vào hai câu lệnh sau:
 ```
 data.iloc[:,0:3] = data.iloc[:,0:3] / 100
 data.iloc[:,3:] = data.iloc[:,3:] / 10
 ```
 ![image](https://user-images.githubusercontent.com/90232557/227149483-e90ff08a-c39d-4719-b020-039e8a742b0d.png)











