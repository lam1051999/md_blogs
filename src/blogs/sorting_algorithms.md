# Các thuật toán sắp xếp cơ bản

<head>
<link rel="preconnect" href="https://fonts.gstatic.com">
<link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@600&display=swap" rel="stylesheet">
</head>
<div style="display: flex; align-items: center;">
<img style="width: 50px; border-radius: 50%; border: 1px solid #b71c1c" src="../images/me.JPG" />
<span style="margin-left: 15px; color: #b71c1c;font-family: 'Cinzel', serif;">Tran Lam</span> <span style="margin-left: 15px;font-family: 'Cinzel', serif;">Feb 18,2021</span> <span style="margin-left: 15px;font-family: 'Cinzel', serif;" >7 min read</span>
</div>
<br/>

Trở lại thôi :satisfied:. Những blogs đầu tiên này mình sẽ chỉ viết về những thuật toán cơ bản nhất khi mới chập chững vào học lập trình thôi. Thứ nhất, để mình học lại các thứ cơ bản (vì mình cực kì hay quên :sob:). Thứ hai, để các bạn mới học lập trình có thể tham khảo ha. Bài viết này sẽ nói về các thuật toán sắp xếp cơ bản mình được học ở trường lớp, và cũng tự học nữa.
### 1. Tại sao chúng ta cần những thuật toán sắp xếp?
**Thứ nhất**, đơn giản là chỉ để qua các kì thi ở trường đại học :satisfied:, học mấy môn Ngôn ngữ lập trình, Cấu trúc dữ liệu và giải thuật,... đi thi dễ bị hỏi mấy cái sắp xếp này lắm luôn.
**Thứ hai**, khâu sắp xếp phần tử thường là khâu trung gian, tiền xử lý dữ liệu trong các bài toán, hệ thống xử lý,... để thực hiện các công việc lớn hơn sau nó. Vì lượng dữ liệu trong các hệ thống thực tế luôn rất lớn, nên ta cần các thuật toán sắp xếp hiệu quả để tốn chi phí nhất (thời gian và bộ nhớ).
**Các ví dụ đơn giản về áp dụng thuật toán sắp xếp**
* Sắp xếp danh sách khách hàng theo tên trong tệp tin quản lý.
* Tìm phần tử trung vị trong \\(\Theta(1)\\), hay là tìm kiếm 1 phần tử nào đó với \\(\Theta(log{_2}{n})\\) nếu như có một mảng đã được sắp xếp.
* Database sử dụng các thuật toán merge sort để sắp xếp các tập dữ liệu khi chúng quá lớn để load cả cục vào bộ nhớ.
* Các trình thiết kế đồ họa cũng sử dụng thuật toán để sắp xếp các tầng (layers) để render thế nào cho hiệu quả.
* Ăn xong cỗ, mẹ bạn bắt bạn rửa bát. Bạn vật lộn với chục chồng bát trong 1 tiếng lận và giờ bạn không muốn mất thêm bất cứ thời gian nào cho đống bát kia nữa. Hóa ra, công việc còn lại là sắp xếp đồng bát vào trạn sao cho ngăn nắp, đẹp và hơn hết là nhanh chóng để bạn còn đi nghịch điện thoại. Theo bản năng của tất cả người châu Á trí thông minh trung bình đổ lên, bạn đã sắp xếp chúng rất nhanh và chồng nhỏ đến chồng to rất bắt mắt, sau đó, bạn nhận ra là mình đã vô tình áp dụng Counting Sort vào việc này.

**Các phép toán cơ bản sử dụng trung gian**
* Phép toán so sánh 2 phần tử \\((a, b)\\), trả về \\(True\\) nếu \\((a > b)\\), trả về \\(False\\) nếu ngược lại.
* Phép toán đổi chỗ 2 phần tử \\((a, b)\\), trong Python sẽ được thực hiện như sau
```python
a, b = b, a
```
Trong quá trình phân tích các thuật toán, ta giả sử rằng các phép toán trên chỉ tốn constant time \\(\Theta(1)\\).

### 2. Sắp xếp nổi bọt (bubble sort)
Sắp xếp nổi bọt là loại sắp xếp đơn giản và kém hiệu quả, thường được dạy trong hầu hêt tất cả các course về thuật toán bởi nó khá trực quan. Sắp xếp nổi bọt so sánh từng cặp số trong một mảng và hoán đổi vị trí cho nhau nếu chúng không theo thứ tự. Những phần tử lớn nhất sẽ được đẩy xuống cuối mảng, trong khi những phần tử nhỏ sẽ dần dần "nổi lên" đầu mảng.

**Thuật toán:**
* So sánh \\(arr[0]\\) với \\(arr[1]\\), nếu \\(arr[0] > arr[1]\\), hoán đổi vị trí của chúng. Tiếp tục làm như vậy cho với (\\(arr[1], arr[2]\\)), (\\(arr[2], arr[3]\\)),...
* Thực hiện bước \\(n\\) lần.

**Phân tích thuật toán:**
* **Best case:** xảy ra khi ta áp dụng thuật toán trên mảng đã được sắp xếp. Khi đó, sẽ không có bước swap nào trong lần duyệt đầu tiên, chỉ có các bước so sánh, từ đó thì thuật toán sẽ kết thúc luôn sau lần duyệt này.
Vì thế, time complexity sẽ là \\(\Theta(n)\\).
Vì lý do này, bubble sort cũng được dùng để kiểm tra xem một mảng đã được sắp xếp hay chưa.
* **Worst case:** xảy ra khi mảng bị sắp xếp theo chiều ngược lại, do đó, có \\(n-1\\) phép so sánh và hoán đổi sẽ được thực hiện trong lần duyệt đầu tiên, \\(n-2\\) phép so sánh và hoán đổi sẽ được thực hiện trong lần duyệt tiếp theo,...
Vì thế, tổng số phép so sánh và hoán đổi sẽ là \\(Sum = (n-1) + (n-2) +...+ 2 + 1 = \frac{n \times (n-1)}{2}\\). Do đó, time complexity sẽ là \\(\Theta(n^2)\\).
* **Space complexity:** \\(\Theta(1)\\).

**Code Python**
```python
ini_arr = [1, 5, 2, 45, 2, 32, 12, 55, 26, 77, 8]

def bubble_sort(arr):
    for i in range(len(arr)):
        swapped = False
        for j in range(len(arr) - i - 1):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
                swapped = True
        if not swapped:
            return

bubble_sort(ini_arr)
print(ini_arr)
```
Output
```python
[1, 2, 2, 5, 8, 12, 26, 32, 45, 55, 77]
```

### 3. Sắp xếp chèn (insertion sort)
Tưởng tượng bạn chơi tiến lên miền Nam, khi mới được phát xong bộ bài trong tay, bạn có nhiều cách sắp xếp tùy theo cá tính của bạn. Với mình, mình thường sắp xếp theo thứ tự quân bài từ bé đến lớn. Những lúc muốn sắp 1 lá bài mới vào bộ quân bài trên tay đã theo thứ tự, mình thực hiện chèn lá bài vào vị trí thích hợp, và đó cũng là ý tưởng của insertion sort.

**Thuật toán:**
Với \\(i = 1, 2,..., n - 1\\), ta sẽ chèn \\(arr[i]\\) vào trong mảng đã sắp xếp \\(arr[0:i-1]\\) bằng việc thực hiện dịch lần lượt các phần tử lớn hơn \\(arr[i]\\) của mảng \\(arr[0:i-1]\\) lên và đặt \\(arr[i]\\) vào đúng vị trí thích hợp.
Để trực quan hơn, mình đem ra hình ảnh mô tả sau

<div style="text-align:center;">
<img style="width: 70%;" src="../images/sorting_algorithms_insertion.GIF" />
</div>

**Phân tích thuật toán:**
* **Best case:** xảy ra khi ta áp dụng thuật toán với mảng đã được sắp xếp. Khi đó, ta chỉ cần duyệt qua 1 lượt mảng, chỉ so sánh và không cần thực hiện một bước hoán đổi nào cả.
Vì thế, time complexity sẽ là \\(\Theta(n)\\).
* **Worst case:** xảy ra khi mảng bị sắp xếp theo chiều ngược lại, sẽ có 1 phép so sánh và gán trong lần duyệt đầu tiên, 2 phép so sánh và gán trong lần dịch thứ hai,...
Vì thế, tổng số phép so sánh và gán sẽ là \\(Sum = 1 + 2 +...+ (n-1) = \frac{n \times (n-1)}{2}\\). Do đó, time complexity sẽ là \\(\Theta(n^2)\\).
* **Space complexity:** \\(\Theta(1)\\).

**Code Python**
```python
ini_arr = [1, 5, 2, 45, 2, 32, 12, 55, 26, 77, 8]

def insertion_sort(arr):
    for key in range(1, len(arr)):
        value = arr[key]
        j = key - 1
        while j >= 0 and value < arr[j]:
            arr[j+1] = arr[j]
            j -= 1
        if key != j+1:
            arr[j+1] = value

insertion_sort(ini_arr)
print(ini_arr)
```
Output
```python
[1, 2, 2, 5, 8, 12, 26, 32, 45, 55, 77]
```

### 4. Sắp xếp lựa chọn (selection sort)
Ý tưởng là ta sẽ **giả định** chia mảng của ta ra làm 2 phần: mảng con được sắp xếp \\(arr{_1}\\) và mảng con chưa được sắp xếp \\(arr{_2}\\). Lúc này, \\(arr = (arr{_1})(arr{_2})\\)
Ta sẽ lần lượt tìm phần tử nhỏ nhất của \\(arr{_2}\\), tách ra và đẩy phần tử đó sang \\(arr{_1}\\). Mình nói **giả định** ở đây là sao, là chúng ta không thực sự tạo ra 2 mảng con mới, mà các hoạt động đều được thực hiện trên mảng gốc.

**Thuật toán:**
* Tìm phần tử nhỏ nhất của \\(arr{_2}\\).
* Hoán đổi vị trí của phần tử nhỏ nhất ấy với phần tử đầu tiên của \\(arr{_2}\\). Lúc này, ta xem như \\(arr{_2}\\) đã không còn phần tử nhỏ nhất đó, và giờ phần từ nhỏ nhất đó đã ghép vào \\(arr{_1}\\).

Mình có hình ảnh để thuật toán thêm trực quan hơn

<div style="text-align:center;">
<img style="width: 70%;" src="../images/sorting_algorithms_selection.PNG" />
</div>

**Phân tích thuật toán:**
* **Best case:** xảy ra khi áp dụng thuật toán trên mảng đã sắp xếp, ta chỉ phải so sánh chứ không cần thực hiện hoán đổi vị trí.
Vì thế, time complexity sẽ là \\(\Theta(n)\\).
* **Worst case:** xảy ra khi mảng trên được sắp xếp theo chiều ngược lại, mỗi lần duyệt ta phải tìm phần tử nhỏ nhất của mảng con \\(arr{_2}\\).
Vì thế, tổng số phép duyệt để tìm các phần tử nhỏ nhất sẽ là \\(Sum = (n-1) + (n-2) +...+ 1 = \frac{n \times (n-1)}{2}\\). Do đó, time complexity sẽ là \\(\Theta(n^2)\\).
* **Space complexity:** \\(\Theta(1)\\).

**Code Python**
```python
ini_arr = [1, 5, 2, 45, 2, 32, 12, 55, 26, 77, 8]

def selection_sort(arr):
    for i in range(len(arr) - 1):
        min_index = i
        for j in range(i+1, len(arr)):
            if arr[j] < arr[min_index]:
                min_index = j
        if i != min_index:
            arr[min_index], arr[i] = arr[i], arr[min_index]

selection_sort(ini_arr)
print(ini_arr)
```
Output
```python
[1, 2, 2, 5, 8, 12, 26, 32, 45, 55, 77]
```

### 5. Sắp xếp trộn (merge sort)
Pending, finish soon, hihi...
**Thuật toán:**
abc
**Phân tích thuật toán:**
* **Best case:** abc
* **Worst case:** abc

**Code Python**
```python
a = b
```
Output
```python
[1, 2, 2, 5, 8, 12, 26, 32, 45, 55, 77]
```

### 6. Sắp xếp vun đống (heap sort)
Pending, finish soon, hihi...
**Thuật toán:**
abc
**Phân tích thuật toán:**
* **Best case:** abc
* **Worst case:** abc

**Code Python**
```python
a = b
```
Output
```python
[1, 2, 2, 5, 8, 12, 26, 32, 45, 55, 77]
```

### 7. Sắp xếp nhanh (quick sort)
Pending, finish soon, hihi...
**Thuật toán:**
abc
**Phân tích thuật toán:**
* **Best case:** abc
* **Worst case:** abc

**Code Python**
```python
a = b
```
Output
```python
[1, 2, 2, 5, 8, 12, 26, 32, 45, 55, 77]
```

### 8. Sắp xếp đếm (counting sort)
Pending, finish soon, hihi...
**Thuật toán:**
abc
**Phân tích thuật toán:**
* **Best case:** abc
* **Worst case:** abc

**Code Python**
```python
a = b
```
Output
```python
[1, 2, 2, 5, 8, 12, 26, 32, 45, 55, 77]
```
# Tài liệu tham khảo
https://www.interviewbit.com/tutorial/sorting-algorithms/#sorting-algorithms
https://brilliant.org/wiki/sorting-algorithms/
