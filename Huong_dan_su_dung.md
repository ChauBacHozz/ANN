# ANN

# Hướng dẫn sử dụng gói ANN để chạy model mạng nơ ron nhân tạo cơ bản (ANN)

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
- scikit-learn: thư viện học máy dùng cho đa mục đích
### Bước 1: Import thư viện vào file code
- Ở đầu file python, nhập vào các dòng sau:
```
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from sklearn.model_selection import train_test_split
from ANN_pkg import *
```
- Từ **as** có nghĩa là ta định nghĩa tên gọi tắt cho thư viện, nhằm giúp cho việc code không bị dài dòng và thuận tiện cho việc gọi các hàm từ thư viện
- import * có nghĩa là ta import tất cả các hàm cần sử dụng từ gói ANN

### Bước 2: Sử dụng python để đọc file dữ liệu và tiến hành tiền xử lý dữ liệu
##### Đọc file dữ liệu
- Copy file dữ liệu (dạng csv, xlsx, txt, ...) vào cùng thư mục với file python
![image](https://user-images.githubusercontent.com/90232557/227155077-a78b36c9-bde0-42ec-bbfa-ee7c52f41242.png)
- Sau đó trong file .py, tạo một biến đặt tên là data (data sẽ lưu trữ thông tin của file dữ liệu) và đọc bảng dữ liệu bằng lệnh pd.read_excel({Tên file})
- Xuống dòng gõ lệnh print(data) rồi chuột phải, chọn "Run Code" để kiểm tra python đã đọc được dữ liệu hay chưa
![image](https://user-images.githubusercontent.com/90232557/227155601-ab8cd4fe-be3c-4b22-b419-3942458f05e9.png)
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
![image](https://user-images.githubusercontent.com/90232557/227156238-f96cd975-fab2-48fb-ba9e-9b23bd211936.png)
 *Sau khi co giãn, ta thấy rằng các giá trị trong bảng dữ liệu đều nằm trong khoảng 0 - 1*
 - Chính quy hóa dữ liệu: với dữ liệu dạng nhiều chiều (nhiều cột) thì việc chính quy hóa giúp cho giá trị của mỗi đặc trưng có trung bình bằng 0 và phương sai bằng 1. Từ đó giúp model dễ dàng tiến được tới giá trị min của hàm loss, đồng thời khiến cho tốc độ học máy tăng lên. Để chính quy hóa dữ liệu ta thêm vào các dòng lệnh sau:
 ```
from sklearn import preprocessing as pp
std = pp.StandardScaler()
data = std.fit_transform(data)
 ```
 
 - Trộn dữ liệu: để mạng ANN học được hết các đặc trưng của tập dữ liệu, trong khoảng thời gian học nó cần phải nhìn thấy các được các dữ liệu khác nhau. Nếu mạng neural được học tập dữ liệu quá giống nhau (Ví dụ: Các phổ trông giống nhau, không có sự khac biệt quá nhiều) sẽ hình thành thiên kiến và sẽ không hoạt động tốt với những dữ liệu nó chưa nhìn thấy bao giờ (overfit). Vì vậy, cần phải thực hiện xáo trộn dữ liệu bằng câu lệnh
 ```
 data = data.sample(frac=1)
 ```
![image](https://user-images.githubusercontent.com/90232557/227151917-499575a0-c2c3-4c6a-a7a1-b78fb792bc39.png)
 
 *Dữ liệu sau khi xáo trộn lẫn nhau*
 #### Lưu ý: Các kỹ thuật tiền xử lý dữ liệu như chuẩn hóa, co giãn, chính quy hóa dữ liệu được sử dụng tùy trong từng trường hợp cụ thể. Với những dữ liệu đặc trưng sẽ phải thử để chọn ra những kỹ thuật sao cho việc học máy được diễn ra một cách tối ưu nhất.
 
 - Tách ma trận dữ liệu thành các cột X và Y, chia thành tập dữ liệu train và test: Ở đây bài toán chính là sử dụng mô hình máy học để sự đoán nồng độ các chất trong hỗn hợp sản phẩm (thuốc) vậy nên mình sẽ coi dữ liệu đầu vào (X) là tín hiệu Abs, còn dữ liệu đích (Y) chính là nồng độ các chất. Chia tập dữ liệu thành tập dữ liệu luyện (train) và tập dữ liệu kiểm tra (test), sử dụng câu lệnh sau:
```
# Nếu trước đó không chuẩn hóa hoặc chính quy hóa dữ liệu
X_train, X_test, y_train, y_test = train_test_split(data.iloc[:,3:], data.iloc[:,0:3],test_size=0.2, random_state=42)
# Nếu trước đó đã chuẩn hóa hoặc chính quy hóa dữ liệu
X_train, X_test, y_train, y_test = train_test_split(data[:,3:], data[:,0:3],test_size=0.2, random_state=42)
```
+ X_train: các cột Abs của tập dữ liệu train
+ y_train: các cột nồng độ của tập dữ liệu train
+ X_test: các cột Abs của tập dữ liệu test
+ y_test: các cột nồng độ của tập dữ liệu test
 
 
 ### Bước 3: Sử dụng mạng ANN để học tập dữ liệu với Batch gradient descent
 - Sau dữ liệu đã được tiền xử lý, chuyển đổi dữ liệu từ dạng Dataframe sang dạn ma trận số và chuyển vị ma trận để truyền vào model:
 ```
X_train = X_train.values.T
y_train = y_train.values.T
X_test = X_test.values.T
y_test = y_test.values.T
 ```
![image](https://user-images.githubusercontent.com/90232557/227165912-ad85a66a-0e64-4606-98d7-5e5c63f2a925.png)
 *Sau khi chuyển đổi, ma trận sẽ có dấu ngoặc vuông ở ngoài*
 - Tạo ra biến có tên là model bằng lệnh Neural_Network():
 ```
 model = Neural_Network([X_train.shape[0], 30, 30, 30, y_train.shape[0]], ReLU)
 ```
 - Cho model luyện với lệnh fit():
 ```
 model.fit(X_train, y_train, learning_rate=0.001, epochs=1000, lr_down=False, lr_decay=20)
 ```
 + Chỉ cho mạng luyện tập với tập dữ liệu train (X_train, y_train) 
 + learning_rate là hệ số học máy, thường sẽ dao động từ khoảng 10E-8 đến 0.1, hệ số học máy phải điều chỉnh thủ công và tùy từng trường hợp dữ liệu thì giá trị của hệ số học máy sẽ khác nhau
 + epochs là số lần học máy, với dữ liệu nhiều chiều và nhiều mẫu thì cần hệ số học máy lớn để model có thể nhận dạng và học hỏi được dữ liệu
 + lr_down, lr_decay là khái niệm tối ưu hệ số học máy trông trường hợp model khó học được tập dữ liệu (hiện tại chưa cần quan tâm)
 - Sau khi đợi model luyện xong, ta có thể xem được quá trình học máy của model có thuận lợi hay không bằng cách kiểm tra sự sai khác giữa giá trị thực và giá trị tính toán (cost) của model bằng câu lệnh:
 ```
 print(np.min(model.cost_his))
 plt.plot(model.cost_his)
 ```
 Thông thường chúng ta trông đợi cost của model đi xuống dần và di chuyển đến nhỏ nhất (min) nào đó, nếu đồ thị không đi xuống dễ dàng hoặc đi ngược lên trên, cần tủy chỉnh lại hệ số học máy đã nói ở trên.
 ![image](https://user-images.githubusercontent.com/90232557/227220797-57e0f4be-53fc-4a42-9ad3-dabc92eb339d.png)
 *Như trường hợp này thì có vẻ như model đã học được tập dữ liệu qua 10000 lần, tuy nhiên phải chuyển lr_down thành True để tối ưu việc tìm đến điểm min, đồng thời ở của sổ terminal hiển thị ra giá trị min và model đạt được, min càng nhỏ so với tập dữ liệu thì khả năng học của model càng tốt.*
 - Sau đó có thể in ra sự đoán của model với tập dữ liệu test (X_test) bằng lệnh:
 ```
 print(model.forward(X_test).T)
 ```
 - Giải thích Batch gradient descent: sử dụng toàn bộ tập dữ liệu train để luyện cho model (Batch) và dùng thuật toán tối ưu gradient descent (có ở trong gói ANN). Điều này khiến cho việc luyện mạng trở nên dễ dàng do model nhìn thấy được toàn bộ tập dữ liệu train, khiến cho cost giảm xuống khá đều trong đồ thị. Tuy nhiên đây cũng là nhược điểm, bởi toàn bộ thời gian thì model chỉ nhìn thấy được dữ liệu train, còn với dữ liệu test nếu có sự khác nhau lớn thì sẽ hoạt động và phán đoán không tốt, điều này gây nên hiện tượng overfit. Để khắc phục cần tăng số lượng dữ liệu (dataset), nhiều mẫu hơn giúp cho model nhìn thấy nhiều dữ liệu hơn, hoặc đổi sang thuật toán tối ưu khác như Mini batch gradient descent.
 

