# Đại số tuyến tính cơ bản - Phần 1

<head>
<link rel="preconnect" href="https://fonts.gstatic.com">
<link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@600&display=swap" rel="stylesheet">
</head>
<div style="display: flex; align-items: center;">
<img style="width: 50px; border-radius: 50%; border: 1px solid #b71c1c" src="../images/us/tranlam.JPG" />
<span style="margin-left: 15px; color: #b71c1c;font-family: 'Cinzel', serif;">Tran Lam</span> <span style="margin-left: 15px;font-family: 'Cinzel', serif;">Feb 20,2021</span> <span style="margin-left: 15px;font-family: 'Cinzel', serif;" >25 min read</span>
</div>
<br/>

Tiếp đây sẽ là loạt bài viết về đại số tuyến tính mình đã học lại khi đọc quyển **[Mathematics for Machine Learning](https://mml-book.github.io/book/mml-book.pdf)** trong thời gian học về Machine Learning và AI. Đây là phần thứ nhất trong loạt bài này.

### Các đề mục

### 1. Giải hệ phương trình tuyến tính
Hệ phương trình tuyến tính là tập các phương trình tuyến tính với cùng những biến số, cấp 2 chúng ta đã giải chán chê phương trình này, thậm chí còn phải làm các hệ phương trình khó nhằn hơn chứa cả biến bậc 2, bậc 3,... Giờ đây, trở lại với đại số tuyến tính, ta có thể mô hình hệ phương trình tuyến tính bậc một với tích của ma trận và véc-tơ tương ứng.
Ví dụ ta có một hệ phương trình đơn giản sau
<div style="text-align:center;">

\\(
\begin{cases} x_{1} \\\;\\\;\\\;\\\;\\\;\\\;\\\;\\\;\\\;\\\; + 8x_{3} - 4x_{4} = 42 \\\\ \\\;\\\;\\\;\\\;\\\;\\\;\\\;\\\;\\\;\\\; x_{2} + 2x_{3} + 12x_{4} = 8 \end{cases}    
\\) 

</div>

Sẽ được viết dưới dạng tích ma trận và véc-tơ biến số như sau
<div style="text-align:center;">

\\(
\begin{bmatrix} 1 & 0 & 8 & -4 \\\\ 0 & 1 & 2 & 12 \end{bmatrix} * \begin{bmatrix} x_{1} \\\\ x_{2} \\\\ x_{3} \\\\ x_{4} \end{bmatrix} = \begin{bmatrix} 42 \\\\ 8 \end{bmatrix}
\\)

\\(
\Leftrightarrow \begin{bmatrix} 1 \\\\ 0 \end{bmatrix} x_{1} + \begin{bmatrix} 0 \\\\ 1 \end{bmatrix} x_{2} + \begin{bmatrix} 8 \\\\ 2 \end{bmatrix} x_{3} + \begin{bmatrix} -4 \\\\ 12 \end{bmatrix} x_{4} = \begin{bmatrix} 42 \\\\ 8 \end{bmatrix} \\\;\\\;\\\;\\\;(1)
\\)

</div>

#### 1.1. Nghiệm chung và nghiệm riêng của phương trình
Nhìn vào biểu thức bên trên \\((1)\\), ta có
- Một nghiệm riêng của hệ phương trình là \\(\begin{bmatrix} 42 & 8 & 0 & 0 \end{bmatrix}^T\\).
- Để có thể thu được tất cả nghiệm thỏa mãn, ta cần phải đi giải phương trình \\(\boldsymbol{Ax = 0}\\) nữa. Ta tiến hành phân tích phương trình \\((1)\\) ra như sau
<div style="text-align:center;">

\\(
\begin{bmatrix} 1 \\\\ 0 \end{bmatrix} x_{1} + \begin{bmatrix} 0 \\\\ 1 \end{bmatrix} x_{2} + 8\begin{bmatrix} 1 \\\\ 0 \end{bmatrix} x_{3} + 2\begin{bmatrix} 0 \\\\ 1 \end{bmatrix} x_{3} + \begin{bmatrix} -4 \\\\ 12 \end{bmatrix} x_{4} = \boldsymbol{0} 
\\)

</div>

Nhìn vào phương trình trên, ta có được một nghiệm cho \\(\boldsymbol{Ax = 0}\\) là \\(\lambda_{1}\begin{bmatrix} 8 & 2 & -1 & 0 \end{bmatrix}^T\\).
Tương tự như trên, ta tìm thêm được một nghiệm cho \\(\boldsymbol{Ax = 0}\\) nữa là \\(\lambda_{2}\begin{bmatrix} -4 & 12 & 0 & -1 \end{bmatrix}^T\\).
Phương trình \\(\boldsymbol{Ax = 0}\\) chỉ có 2 nghiệm, tại sao lại như vậy thì bên dưới mình sẽ nói sau.
Như vậy, hệ phương trình có nghiệm chung là 
<div style="text-align:center;">

\\(
    \\{ x \in \Bbb R^4: x = \begin{bmatrix} 42 \\\\ 8 \\\\ 0 \\\\ 0 \end{bmatrix} + \lambda_{1}\begin{bmatrix} 8 \\\\ 2 \\\\ -1 \\\\ 0 \end{bmatrix} + \lambda_{2}\begin{bmatrix} -4 \\\\ 12 \\\\ 0 \\\\ -1 \end{bmatrix}, \lambda_{1}, \lambda_{2} \in \Bbb R \\}
\\)

</div>

#### 1.2. Biến đổi ma trận
##### 1.2.1. Ví dụ
Mình sẽ đem một ví dụ cho phương pháp này
<div style="text-align:center;">

\\(
\begin{cases} 
-2x_{1} + 4x_{2} - 2x_{3} - x_{4} + 4x_{5} = -3 \\\\
4x_{1} - 8x_{2} + 3x_{3} - 3x_{4} + x_{5} = 2 \\\\
x_{1} - 2x_{2} + x_{3} - x_{4} + x_{5} = 0 \\\\
x_{1} - 2x_{2} \\\;\\\;\\\;\\\;\\\;\\\;\\\;\\\; - 3x_{4} + x_{5} = a \\\\
\end{cases}    
\\) 

</div>

Viết thành dạng
<div style="text-align:center;">

\\(
\left[
  \begin{matrix}
    -2 & 4 & -2 & -1 & 4 \\\\
    4 & -8 & 3 & -3 & 1 \\\\
    1 & -2 & 1 & -1 & 1 \\\\
    1 & -2 & 0 & -3 & 1 \\\\
  \end{matrix}
\left|
\begin{matrix}
    -3  \\\\
    2  \\\\
    0  \\\\
    a  \\\\
\end{matrix}
\right.
\right]
\\)

\\(
\rightsquigarrow ... \rightsquigarrow
\left[
  \begin{matrix}
    1 & -2 & 1 & -1 & 1 \\\\
    0 & 0 & 1 & -1 & 3 \\\\
    0 & 0 & 0 & 1 & -2 \\\\
    0 & 0 & 0 & 0 & 0 \\\\
  \end{matrix}
\left|
\begin{matrix}
    0  \\\\
    -2  \\\\
    1  \\\\
    a+1  \\\\
\end{matrix}
\right.
\right]
\\)

</div>

Do vậy, hệ phương trình được giải khi \\(a = -1\\).
- Nghiệm riêng của phương trình là \\(\begin{bmatrix} 2 & 0 & -1 & 1 & 0 \end{bmatrix}^T\\).
- Nghiệm của phương trình \\(\boldsymbol{Ax = 0}\\) là \\(\lambda_{1}\begin{bmatrix} 2 & 1 & 0 & 0 & 0 \end{bmatrix}^T\\) và \\(\lambda_{2}\begin{bmatrix} -2 & 0 & 1 & -2 & -1 \end{bmatrix}^T\\).

Như vậy, nghiệm chung của phương trình là 
<div style="text-align:center;">

\\(
    \\{ x \in \Bbb R^5: x = \begin{bmatrix} 2 \\\\ 0 \\\\ -1 \\\\ 1 \\\\ 0 \end{bmatrix} + \lambda_{1}\begin{bmatrix} 2 \\\\ 1 \\\\ 0 \\\\ 0 \\\\ 0 \end{bmatrix} + \lambda_{2}\begin{bmatrix} -2 \\\\ 0 \\\\ 1 \\\\ -2 \\\\ -1 \end{bmatrix}, \lambda_{1}, \lambda_{2} \in \Bbb R \\}
\\)

</div>


##### 1.2.2. Ma trận bậc thang
Một ma trận ở dạng bậc thang nếu
- Những hàng chỉ chứa 0 sẽ ở đáy ma trận. Những hàng chứa ít nhất 1 số khác không sẽ nằm trên các hàng chứa toàn 0.
- Các phần tử pivot của mỗi hàng luôn ở phía bên phải của các phần tử pivot ở các hàng bên trên.

Các biến ứng với các phần tử pivot là các basic variables, các biến còn lại là free variables.

Với hệ phương trình tuyến tính \\(\boldsymbol{Ax = b}\\), để tính toán một nghiệm riêng, ta biểu diễn các \\(\boldsymbol{b} = \sum_{i = 1}^p \lambda_{i}\boldsymbol{p_{i}}\\) với \\(\boldsymbol{p_{i}}\\) là các pivot columns, chúng ta thường bắt đầu ước lượng các giá trị \\(\lambda_{i}\\) với các pivot columns từ phải sang trái.

Một ma trận ở dạng bậc thang tối giản nếu
- Nó là một ma trận bậc thang.
- Các phần tử pivot đều bằng 1.
- Phần tử pivot là phần tử duy nhất khác 0 tại pivot column đó.

Việc tính toán nghiệm \\(\boldsymbol{Ax = 0}\\) sẽ dễ dàng hơn rất nhiều nếu ma trận biểu diễn hệ phương trình tuyến tính ở dạng bậc thang tối giản 

##### 1.2.3. Phép khử Gaussian
Là một thuật toán biểu diễn các phép biến đổi triệt tiêu giữa các hàng để đưa ma trận biểu diễn hệ phương trình tuyến tính về dạng ma trận bậc thang tối giản.

Để tính toán nghiệm của \\(\boldsymbol{Ax = 0}\\) trong ma trận bậc thang tối giản, ta biểu diễn các pivot column bằng tổng các cấp số của các pivot columns ở bên trái của chúng.

Ví dụ với ma trận bậc thang sau
<div style="text-align:center;">

\\(
\boldsymbol{A} = 
\begin{bmatrix} 
1 & 3 & 0 & -4 & 0 \\\\ 
0 & 0 & 1 & -3 & 0 \\\\
0 & 0 & 0 & 0 & 1 \\\\
0 & 0 & 0 & 0 & 0 \\\\
\end{bmatrix}
\\)

</div>

Nghiệm của phương trình \\(\boldsymbol{Ax = 0}\\) là
<div style="text-align:center;">

\\(
    \\{ x \in \Bbb R^5: x = \lambda_{1}\begin{bmatrix} 3 \\\\ -1 \\\\ 0 \\\\ 0 \\\\ 0 \end{bmatrix} + \lambda_{2}\begin{bmatrix} -4 \\\\ 0 \\\\ -3 \\\\ -1 \\\\ 0 \end{bmatrix}, \lambda_{1}, \lambda_{2} \in \Bbb R \\}
\\)

</div>

#### 1.3. The -1 trick
Với ma trận \\(\boldsymbol{A}\\) ở trên, ta sẽ chêm các hàng gồm toàn \\(0\\) và chỉ một số \\(-1\\) vào giữa các hàng của ma trận bậc thang tối giản, để tạo nên ma trận mới có đường chéo chính gồm toàn \\(-1\\) và \\(1\\) như dưới đây.

<div style="text-align:center;">

\\( 
\boldsymbol{A} \rightsquigarrow
\begin{bmatrix} 
1 & 3 & 0 & -4 & 0 \\\\ 
0 & -1 & 0 & 0 & 0 \\\\
0 & 0 & 1 & -3 & 0 \\\\
0 & 0 & 0 & -1 & 0 \\\\
0 & 0 & 0 & 0 & 1 \\\\
\end{bmatrix}
\\)

</div>

Từ đó, các cột chứa giá trị \\(-1\\) tại các vị trí trên đường chéo chính của ma trận sẽ là nghiệm của phương trình \\(\boldsymbol{Ax = 0}\\).


#### 1.4. Một số thuật toán để giải hệ phương trình này
Có một số thuật toán thông dụng để giải hệ phương trình tuyến tính phức tạp
- Sử dụng thuật toán hồi quy tuyến tính (linear regression), thuật toán này thường áp dụng vào các bài toán mà ta chỉ có thể tính xấp xỉ nghiệm của phương trình.
- Normal equation, thuật toán này tính chính xác nghiệm của hệ phương trình, nhưng số lượng tính toán rất nhiều nên không thể sử dụng với các trường hợp số lượng biến nhiều. Phương pháp này được thể hiện dưới đây
<div style="text-align:center;">

\\(
    \boldsymbol{Ax = b} \Leftrightarrow \boldsymbol{A^TAx = A^Tb} \Leftrightarrow \boldsymbol{x = (A^TA)^{-1}A^Tb}
\\)

</div>

Việc phải nhân ma trận và tính toán nghịch đảo khiến phương pháp này có độ phức tập là \\(\Theta(n^3)\\).

### 2. Không gian véc-tơ

#### 2.1. Nhóm

#### 2.2. Không gian véc-tơ

#### 2.3. Không gian véc-tơ con

### 3. Phụ thuộc tuyến tính

### 3.1. Linear combination

### 3.2. Phụ thuộc tuyến tính

### 4. Cơ sở và rank

#### 4.1. Hệ sinh của một không gian véc-tơ

#### 4.2. Cơ sở của một không gian véc-tơ

#### 4.3. Rank của một ma trận

### 5. Ánh xạ tuyến tính

#### 5.1. Biểu diễn ánh xạ tuyến tính dưới dạng ma trận

#### 5.2. Chuyển đổi cơ sở

#### 5.3. Image và kernel

### 6. Không gian véc-tơ Affine

#### 6.1. Không gian véc-tơ affine con

#### 6.2. Ánh xạ Affine






