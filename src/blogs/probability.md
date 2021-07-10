# Xác suất thống kê cơ bản

<head>
<link rel="preconnect" href="https://fonts.gstatic.com">
<link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@600&display=swap" rel="stylesheet">
<style>
#t01 {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}
#t01 td, #t01 th {
  border: 1px solid #ddd;
  padding: 8px;
}
#t01 tr:nth-child(even){background-color: #f2f2f2;}
#t01 tr:hover {background-color: #ddd;}
#t01 th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: center;
  background-color: #04AA6D;
  color: white;
}
</style>
</head>
<div style="display: flex; align-items: center;">
<img style="width: 50px; border-radius: 50%; border: 1px solid #b71c1c" src="../images/us/tranlam.JPG" />
<span style="margin-left: 15px; color: #b71c1c;font-family: 'Cinzel', serif;">Tran Lam</span> <span style="margin-left: 15px;font-family: 'Cinzel', serif;">July 04,2021</span> <span style="margin-left: 15px;font-family: 'Cinzel', serif;" >15 min read</span>
</div>
<br/>

Bài viết này nhằm ôn lại một số khái niệm trong toán xác suất cơ bản, sẽ không có những phần toán rất phức tạp và dồn dập như trong lúc học trên trường lớp. Thay vào đó, nội dung sẽ tập trung vào các kiến thức xác suất phụ trợ cho trí tuệ nhận tạo hay là thống kê dữ liệu. Bài viết này tham chiếu rất nhiều đến một bài trong blog của anh Phạm Đình Khánh, cảm ơn anh Khánh với một series xác suất rất chi tiết.

### Các đề mục
[1. Đôi chút về đánh giá dữ liệu](#1-Đôi-chút-về-đánh-giá-dữ-liệu)

[2. Các kiểu dữ liệu](#2-các-kiểu-dữ-liệu)

[3. Các hàm xác suất](#3-các-hàm-xác-suất)

[4. Các loại biểu đồ thống kê](#4-các-loại-biểu-đồ-thống-kê)

[5. Độ lệch dương, độ lệch âm](#5-Độ-lệch-dương-độ-lệch-âm)

[6. Quy luật số lớn](#6-quy-luật-số-lớn)

[7. Các phân phối xác suất](#7-các-phân-phối-xác-suất)

[8. Xác suất đồng thời, xác suất biên, xác suất có điều kiện và định lỹ Bayes](#8-xác-suất-đồng-thời-xác-suất-biên-xác-suất-có-điều-kiện-và-định-lỹ-bayes)

[9. Tài liệu tham khảo](#9-tài-liệu-tham-khảo)


### 1. Đôi chút về đánh giá dữ liệu
Khi đánh giá dữ liệu, ta thường quan tâm đến các tiêu chí để đo đạc độ tập trung (measure of central tendency) cũng như độ phân tán (dispersion) của dữ liệu.

Về độ tập trung của dữ liệu, có 3 thông số cần quan tâm

- Kỳ vọng (mean): đánh giá giá trị trung bình của một biến ngẫu nhiên.

    - Nếu \\(x\\) là một biến ngẫu nhiên rời rạc, giá trị kỳ vọng được tính như sau
        <div style="text-align:center;">

        \\(E(x) = \sum_{i=1}^{n}x_{i}p(x_{i}) \\)

        </div>
        
        Trong đó, \\(p(x_{i})\\) là xác suất khi mà biến ngẫu nhiên \\(x\\) nhận giá trị \\(x_{i}\\).

    - Nếu \\(x\\) là một biến ngẫu nhiên liên tục
        <div style="text-align:center;">

        \\(E(x) = \int xp(x)dx \\)

        </div>

    Từ đó, ta có một số tính chất của kỳ vọng như sau
            <div style="text-align:center;">
            \\(E(ax + by) = aE(x) + bE(y) \\)
            </div>
            <div style="text-align:center;">
            \\(E(xy) = E(x)E(y)\\), nếu hai biến \\(x\\) và \\(y\\) độc lập
            </div>

- Trung vị (median): là giá trị của phần tử nằm ở chính giữa một dãy giá trị được sắp xếp theo thứ tự. Trường hợp số phần tử là chẵn, giá trị trung vị bằng trung bình cộng 2 phần tử ở giữa.

- Mode: giá trị phần tử có tần số xuất hiện nhiều nhất trong dãy giá trị.

    Ví dụ, ta có dãy giá trị của một biến ngẫu nhiên qua các sự kiện là \\(\\{1, 1, 2, 4, 6, 6, 6, 14\\}\\) với các sự kiện có xác suất xảy ra như nhau
        <div style="text-align:center;">
        \\(Mean = \frac{1+1+2+4+6+6+6+14}{8} = 5\\), \\(Median = \frac{4+6}{2} = 5\\), \\(Mode = 6\\)
        </div>
        
    Nếu thêm một giá trị nữa vào dãy \\(\\{1, 1, 2, 4, 6, 6, 6, 14, 500\\}\\)
        <div style="text-align:center;">
        \\(Mean = \frac{1+1+2+4+6+6+6+14+500}{9} = 60\\), \\(Median = 6\\), \\(Mode = 6\\)
        </div>
    Ta nhận thấy rằng, giá trị mean chịu ảnh hưởng nặng bởi các outliers hơn là median (các outliers sẽ được giải thích ở dưới).

Về độ phân tán của dữ liệu, ta quan tâm đến các đại lượng sau

- Phương sai: thể hiện mức độ biến động của đại lượng xung quanh giá trị kỳ vọng.

    - Nếu \\(x\\) là một biến ngẫu nhiên rời rạc
    <div style="text-align:center;">

    \\(Var(x) = \sum_{i=1}^{n}(x_{i} - E(x))^2p(x_{i}) \\)

    </div>

    - Nếu \\(x\\) là một biến ngẫu nhiên liên tục
    <div style="text-align:center;">

    \\(Var(x) = \int(x - E(x))^2p(x)dx \\)

    </div>

- Độ lệch chuẩn: bằng căn bậc hai của phương sai
    <div style="text-align:center;">

    \\(\sigma_x = \sqrt{Var(x)} \\)

    </div>

    Các outliers là những giá trị nằm ngoài khoảng \\([\mu - 3\sigma_x, \mu + 3\sigma_x]\\) với \\(\mu = E(x)\\). Trong chọn lọc các đặc trưng tốt cho học máy, các outliers thường bị lọc bỏ bởi nó có nguy cơ là những điểm gây nhiễu cao.

Tìm ra các đặc trưng của tập dữ liệu, người ta còn hay quan tâm đến các thông số trên đồ thị box plot
<div style="text-align:center;">
<img style="width: 70%;" src="../images/probability/boxplot.PNG" />
</div>

Ở hình trên, median là giá trị trung vị, \\(Q1\\) và \\(Q3\\) lần lượt là các giá trị trung vị \\(25\\%\\) và \\(75\\%\\), độ trải giữa (\\(IQR)\\) là khoảng các giữa chúng. Các điểm nằm ngoài khoảng \\([Q1 - 1.5IQR, Q3 + 1.5IQR]\\) được coi là các mild outliers, nằm ngoài khoảng \\([Q1 - 3IQR, Q3 + 3IQR]\\) được coi là các extreme outliers. Các outliers thường được loại bỏ khỏi dữ liệu khi mà ta muốn phân tích thông tin gì đó từ dữ liệu.

Để đánh giá tương quan tuyến tính giữa 2 biến ngẫu nhiên, ta quan tâm đến đại lượng hệ số tương quan. Giá trị của hệ số tương quan thường trải từ khoảng \\([-1, 1]\\). Công thức tính hệ số tương quan như sau
<div style="text-align:center;">

\\(\rho_{xy} = \frac{cov(x, y)}{\sigma_x\sigma_y}\\), với \\(cov(x, y) = E[(x - \mu_x)(y - \mu_y)] = \frac{\sum_{i = 1}^{n}(x_{i} - \mu_x)(y_{i} - \mu_y)}{n}\\), \\(\sigma\\) và \\(\mu\\) lần lượt là độ lệch chuẩn và kỳ vọng của biến ngẫu nhiên.
</div>

Ta có một vài nhận xét như sau
- Khi \\(\rho_{xy} = 0\\), hai biến ngẫu nhiên hoàn toàn độc lập tuyến tính với nhau.
- Khi \\(\rho_{xy} > 0\\), chúng đồng biến, biến đầu tiên tăng thì biến thứ hai cũng tăng.
- Khi \\(\rho_{xy} < 0\\), chúng nghịch biến, biến đầu tiên tăng thì biến thứ hai giảm.
- Khi \\(\rho_{xy}\\) bằng \\(-1\\) hoặc \\(1\\), hai biến hoàn toàn tương quan tuyến tính. 

### 2. Các kiểu dữ liệu
Có nhiều loại kiểu dữ liệu mà một biến ngẫu nhiên có thể nhận, tùy vào bài toán nhất định, ta có thể giữ nguyên giá trị các biến trong tính toán, hoặc mã hóa nó.
- Kiểu dữ liệu định tính (quanlitative data): là các kiểu dữ liệu mang thông tin mô tả đặc trưng của sự vật, hiện tượng.
    - Các kiểu dữ liệu định tính không có thứ tự (nominal data): màu sắc, giới tính,... Với loại dữ liệu này, ta thường dùng mode để đánh giá chúng. Ví dụ như: đánh giá màu xe con nào xuất hiện nhiều nhất,...
    - Các kiểu dữ liệu định tính có thứ tự (ordinal data): các mức độ, các cấp học như tiểu học, trung học cơ sở, trung học phổ thông,... Với loại dữ liệu này, ta quan tâm nhiều hơn đến thông số median. Ví dụ như: đánh gía mức độ trung bình trong tập dữ liệu,...
- Kiểu dữ liệu định lượng (quantitative data): là các thông tin mô tả đối tượng dưới dạng con số. Với loại dữ liệu này, ta dùng các giá trị mean và median để đánh giá chúng.
    - Dữ liệu liên tục (continous data): chiều cao, cân nặng,...
    - Dữ liệu rời rạc (discrete data): số chiếc áo, số bánh xe,...
- Kiểu dữ liệu kèm theo yếu tố thời gian (temporal data): ví dụ như giá cổ phiếu, khi báo cáo cần phải đi kèm với thông tin là ngày nào, thời điểm nào,...
- Kiểu dữ liệu kèm theo yếu tố không gian (spartial data): ví dụ như vị trí địa lý trên bản đồ, giá trị tọa độ của một điểm trên trục tọa độ,...

### 3. Các hàm xác suất
Các hàm xác suất các bạn có thể xem **[tại đây](https://phamdinhkhanh.github.io/deepai-book/ch_probability/appendix_probability.html#ham-mat-do-pdf-va-ham-khoi-xac-suat-pmf)**, cảm ơn anh Phạm Đình Khánh đã viết rất chi tiết về các hàm này.

### 4. Các loại biểu đồ thống kê
Tùy theo mục đích thông tin ta cần trích xuất từ dữ liệu mà ta sẽ sử dụng các loại biểu đồ phù hợp cho bài toán
<table id="t01">
  <tr>
    <th>Mục đích</th>
    <th>Biểu đồ</th>
  </tr>
  <tr>
    <th colspan="2">Cần nhìn bức tranh tổng thể của dữ liệu</th>
  </tr>
  <tr>
    <td>Biểu diễn phân bố dữ liệu, với trục hoành là các khoảng giá trị biến ngẫu nhiên và trục tung là giá trị tần số xuất hiện của chúng</td>
    <td>
        <div style="text-align:center;">
            Histogram plot
        <img style="width: 90%;" src="../images/probability/histogramplot.PNG" />
        </div>
    </td>
  </tr>
  <tr>
    <td>
    Biểu diễn các giá trị quan trọng như min, max, trung vị 25%, 50%, 75%, độ trải giữa IQR,... Từ đó, ta đánh giá được các điểm chia cắt dữ liệu hay các điểm dữ liệu gây nhiễu,...</td>
    <td>
        <div style="text-align:center;">
            Box plot 
        <img style="width: 90%;" src="../images/probability/boxplot.PNG" />
        </div>
    </td>
  </tr>
  <tr>
    <td>Biểu diễn dữ liệu theo thời gian</td>
    <td>
        <div style="text-align:center;">
            Time series plot
        <img style="width: 90%;" src="../images/probability/timeseriesplot.PNG" />
        </div>
    </td>
  </tr>
  <tr>
    <th colspan="2">Cần biểu diễn sự so sánh giữa các biến</th>
  </tr>
  <tr>
    <td>So sánh giá trị của nhiều biến</td>
    <td>
        <div style="text-align:center;">
            Bar chart
        <img style="width: 90%;" src="../images/probability/barchart.PNG" />
        </div>
    </td>
  </tr>
  <tr>
    <td>So sánh giá trị một biến thay đổi theo thời gian</td>
    <td>
        <div style="text-align:center;">
            Line chart, giống với timeseriesplot
        </div>
    </td>
  </tr>
  <tr>
    <td>So sánh nhiều nhóm</td>
    <td>
        <div style="text-align:center;">
            Radar chart
        <img style="width: 90%;" src="../images/probability/radarchart.PNG" />
        </div>
    </td>
  </tr>
  <tr>
    <th colspan="2">Cần nhận biết sự tương quan giữa hai hoặc nhiều biến</th>
  </tr>
  <tr>
    <td>Tương quan giữa hai hoặc nhiều biến</td>
    <td>
        <div style="text-align:center;">
            Scatter plot
        <img style="width: 90%;" src="../images/probability/scatterplot.JPG" />
        </div>
    </td>
  </tr>
</table> 

### 5. Độ lệch dương, độ lệch âm
- Độ lệch dương có giá trị trung bình (mean) lớn hơn giá trị trung vị (median) và phân bố có phía không đối xứng mở rộng đến nhiều các giá trị dương hơn.

<div style="text-align:center;">
<img style="width: 60%;" src="../images/probability/positiveskewness.PNG" />
</div>

- Độ lệch âm có giá trị trung bình (mean) nhỏ hơn giá trị trung vị (median) và phân bố có phía không đối xứng mở rộng đến nhiều các giá trị âm hơn.

<div style="text-align:center;">
<img style="width: 60%;" src="../images/probability/negativeskewness.JPG" />
</div>

Độ lệch kết hợp với độ nhọn đánh giá khả năng các biến cố rơi vào đuôi của phân phối xác suất tốt hơn.

### 6. Quy luật số lớn
Phần này các bạn hãy tham khảo **[tại đây](https://phamdinhkhanh.github.io/deepai-book/ch_probability/appendix_probability.html#qui-luat-so-lon)** của anh Phạm Đình Khánh.

- Khoảng tin cậy (confidence interval)

Khi mình lấy mẫu từ một quần thể, các tham số của một quần thể có thể được đánh giá bằng mẫu đó. Thông thường, giá trị kỳ vọng của mẫu sẽ được ước lượng bằng giá trị kỳ vọng của quần thể, tuy nhiên, những lần lấy mẫu khác nhau thì có kỳ vọng khác nhau. Do vậy, ta đưa ra định nghĩa khoảng tin cậy dùng để biến cái tham số kỳ vọng được ước lượng trở thành một khoảng giá trị ước lượn, đảm bảo rằng kỳ vọng của quần thể sẽ nằm trong khoảng giá trị đó.

\\(k\\%\\) mức tin cậy sẽ đảm bảo phủ được tham số kỳ vọng cần ước lượng của quần thể với kác suất là \\(k\\%\\).

Khoảng tin cậy càng nhỏ thì càng đảm bảo được độ chính xác của bộ ước lượng, để đạt được điều này, ta có thể giảm mức tin cậy hoặc tăng kích thước của mẫu lấy từ quần thể. Khoảng tin cậy được biểu diễn bởi \\((lower bound, upper bound)\\) với

<div style="text-align:center;">

\\(lower bound = \bar{x} - z\frac{\sigma}{\sqrt{n}}\\)

\\(upper bound = \bar{x} + z\frac{\sigma}{\sqrt{n}}\\)

</div>

Với \\(\bar{x}\\) là giá trị kỳ vọng của mẫu được lấy, \\(\sigma\\) là giá trị độ lệch chuẩn giá định của quần thể. \\(n\\) là kích thước của mẫu và \\(z\\) là hệ số tin cậy.

Với phân phối chuẩn
- \\(z = 1.645\\) ứng với mức tin cậy \\(90\\%\\).
- \\(z = 1.96\\) ứng với mức tin cậy \\(95\\%\\).
- \\(z = 2.576\\) ứng với mức tin cậy \\(99\\%\\).

### 7. Các phân phối xác suất
Các phân phối xác suất các bạn có thể xem **[tại đây](https://phamdinhkhanh.github.io/deepai-book/ch_probability/appendix_probability.html#phan-phoi-xac-suat)**, một lần nữa cảm ơn anh Phạm Đình Khánh đã trình bày chi tiết về phần này.

### 8. Xác suất đồng thời, xác suất biên, xác suất có điều kiện và định lỹ Bayes
Các bạn có thể tìm thấy thông tin mục này **[tại đây](https://phamdinhkhanh.github.io/deepai-book/ch_probability/appendix_probability.html#xac-suat-dong-thoi-join-distribution)**.

### 9. Tài liệu tham khảo

[https://phamdinhkhanh.github.io/deepai-book/ch_probability/appendix_probability.html#phan-phoi-xac-suat](https://phamdinhkhanh.github.io/deepai-book/ch_probability/appendix_probability.html#)
