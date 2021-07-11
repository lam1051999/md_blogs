# Đại số tuyến tính cơ bản - Phần 1

<head>
<link rel="preconnect" href="https://fonts.gstatic.com">
<link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@600&display=swap" rel="stylesheet">
</head>
<div style="display: flex; align-items: center;">
<img style="width: 50px; border-radius: 50%; border: 1px solid #b71c1c" src="../images/us/tranlam.JPG" />
<span style="margin-left: 15px; color: #b71c1c;font-family: 'Cinzel', serif;">Tran Lam</span> <span style="margin-left: 15px;font-family: 'Cinzel', serif;">July 10,2021</span> <span style="margin-left: 15px;font-family: 'Cinzel', serif;" >25 min read</span>
</div>
<br/>

Tiếp đây sẽ là loạt bài viết về đại số tuyến tính mình đã học lại khi đọc quyển **[Mathematics for Machine Learning](https://mml-book.github.io/book/mml-book.pdf)** trong thời gian học về Machine Learning và AI. Đây là phần thứ nhất trong loạt bài này.

### Các đề mục
[1. Giải hệ phương trình tuyến tính](#1-giải-hệ-phương-trình-tuyến-tính)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1.1. Nghiệm chung và nghiệm riêng của phương trình](#11-nghiệm-chung-và-nghiệm-riêng-của-phương-trình)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1.2. Biến đổi ma trận](#12-biến-đổi-ma-trận)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1.2.1. Ví dụ](#121-ví-dụ)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1.2.2. Ma trận bậc thang](#122-ma-trận-bậc-thang)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1.2.3. Phép khử Gaussian](#123-phép-khử-gaussian)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1.3. The -1 trick](#13-the--1-trick)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[1.4. Một số thuật toán để giải hệ phương trình này](#14-một-số-thuật-toán-để-giải-hệ-phương-trình-này)

[2. Không gian véc-tơ](#2-không-gian-véc-tơ)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2.1. Nhóm](#21-nhóm)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2.2. Không gian véc-tơ](#22-không-gian-véc-tơ)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[2.3. Không gian véc-tơ con](#23-không-gian-véc-tơ-con)

[3. Phụ thuộc tuyến tính](#3-phụ-thuộc-tuyến-tính)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3.1. Tổ hợp tuyến tính](#31-tổ-hợp-tuyến-tính)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[3.2. Phụ thuộc tuyến tính](#32-phụ-thuộc-tuyến-tính)

[4. Cơ sở và rank](#4-cơ-sở-và-rank)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4.1. Hệ sinh của một không gian véc-tơ](#41-hệ-sinh-của-một-không-gian-véc-tơ)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4.2. Cơ sở của một không gian véc-tơ](#42-cơ-sở-của-một-không-gian-véc-tơ)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[4.3. Rank của một ma trận](#43-rank-của-một-ma-trận)

[5. Ánh xạ tuyến tính](#5-Ánh-xạ-tuyến-tính)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5.1. Biểu diễn ánh xạ tuyến tính dưới dạng ma trận](#51-biểu-diễn-ánh-xạ-tuyến-tính-dưới-dạng-ma-trận)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5.2. Chuyển đổi cơ sở](#52-chuyển-đổi-cơ-sở)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[5.3. Image và kernel](#53-image-và-kernel)

[6. Không gian véc-tơ Affine](#6-không-gian-véc-tơ-affine)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6.1. Không gian véc-tơ affine con](#61-không-gian-véc-tơ-affine-con)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[6.2. Ánh xạ Affine](#62-Ánh-xạ-affine)



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
- Để có thể thu được tất cả nghiệm thỏa mãn, ta cần phải đi giải phương trình \\(\boldsymbol{Ax} = \boldsymbol{0}\\) nữa. Ta tiến hành phân tích phương trình \\((1)\\) ra như sau
<div style="text-align:center;">

\\(
\begin{bmatrix} 1 \\\\ 0 \end{bmatrix} x_{1} + \begin{bmatrix} 0 \\\\ 1 \end{bmatrix} x_{2} + 8\begin{bmatrix} 1 \\\\ 0 \end{bmatrix} x_{3} + 2\begin{bmatrix} 0 \\\\ 1 \end{bmatrix} x_{3} + \begin{bmatrix} -4 \\\\ 12 \end{bmatrix} x_{4} = \boldsymbol{0} 
\\)

</div>

Nhìn vào phương trình trên, ta có được một nghiệm cho \\(\boldsymbol{Ax} = \boldsymbol{0}\\) là \\(\lambda_{1}\begin{bmatrix} 8 & 2 & -1 & 0 \end{bmatrix}^T\\).
Tương tự như trên, ta tìm thêm được một nghiệm cho \\(\boldsymbol{Ax} = \boldsymbol{0}\\) nữa là \\(\lambda_{2}\begin{bmatrix} -4 & 12 & 0 & -1 \end{bmatrix}^T\\).
Phương trình \\(\boldsymbol{Ax} = \boldsymbol{0}\\) chỉ có 2 nghiệm, tại sao lại như vậy thì bên dưới mình sẽ nói sau.
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
- Nghiệm của phương trình \\(\boldsymbol{Ax} = \boldsymbol{0}\\) là \\(\lambda_{1}\begin{bmatrix} 2 & 1 & 0 & 0 & 0 \end{bmatrix}^T\\) và \\(\lambda_{2}\begin{bmatrix} -2 & 0 & 1 & -2 & -1 \end{bmatrix}^T\\).

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

Với hệ phương trình tuyến tính \\(\boldsymbol{Ax} = \boldsymbol{b}\\), để tính toán một nghiệm riêng, ta biểu diễn các \\(\boldsymbol{b} = \sum_{i = 1}^p \lambda_{i}\boldsymbol{p_{i}}\\) với \\(\boldsymbol{p_{i}}\\) là các pivot columns, chúng ta thường bắt đầu ước lượng các giá trị \\(\lambda_{i}\\) với các pivot columns từ phải sang trái.

Một ma trận ở dạng bậc thang tối giản nếu
- Nó là một ma trận bậc thang.
- Các phần tử pivot đều bằng 1.
- Phần tử pivot là phần tử duy nhất khác 0 tại pivot column đó.

Việc tính toán nghiệm \\(\boldsymbol{Ax} = \boldsymbol{0}\\) sẽ dễ dàng hơn rất nhiều nếu ma trận biểu diễn hệ phương trình tuyến tính ở dạng bậc thang tối giản 

##### 1.2.3. Phép khử Gaussian
Là một thuật toán biểu diễn các phép biến đổi triệt tiêu giữa các hàng để đưa ma trận biểu diễn hệ phương trình tuyến tính về dạng ma trận bậc thang tối giản.

Để tính toán nghiệm của \\(\boldsymbol{Ax} = \boldsymbol{0}\\) trong ma trận bậc thang tối giản, ta biểu diễn các pivot column bằng tổng các cấp số của các pivot columns ở bên trái của chúng.

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

Nghiệm của phương trình \\(\boldsymbol{Ax} = \boldsymbol{0}\\) là
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

Từ đó, các cột chứa giá trị \\(-1\\) tại các vị trí trên đường chéo chính của ma trận sẽ là nghiệm của phương trình \\(\boldsymbol{Ax} = \boldsymbol{0}\\).


#### 1.4. Một số thuật toán để giải hệ phương trình này
Có một số thuật toán thông dụng để giải hệ phương trình tuyến tính phức tạp
- Sử dụng thuật toán hồi quy tuyến tính (linear regression), thuật toán này thường áp dụng vào các bài toán mà ta chỉ có thể tính xấp xỉ nghiệm của phương trình.
- Normal equation, thuật toán này tính chính xác nghiệm của hệ phương trình, nhưng số lượng tính toán rất nhiều nên không thể sử dụng với các trường hợp số lượng biến nhiều. Phương pháp này được thể hiện dưới đây
<div style="text-align:center;">

\\(
    \boldsymbol{Ax} = \boldsymbol{b} \Leftrightarrow \boldsymbol{A^TAx} = \boldsymbol{A^Tb} \Leftrightarrow \boldsymbol{x} = \boldsymbol{(A^TA)^{-1}A^Tb}
\\)

</div>

Việc phải nhân ma trận và tính toán nghịch đảo khiến phương pháp này có độ phức tập là \\(\Theta(n^3)\\).

### 2. Không gian véc-tơ

#### 2.1. Nhóm
Cho một tập \\(\mathcal{G}\\) với phép toán \\(\otimes: \mathcal{G} \times \mathcal{G} \to \mathcal{G}\\) được định nghĩa trên \\(\mathcal{G}\\) thì \\(\mathcal{G} := (\mathcal{G}, \otimes)\\) được gọi là một nhóm nếu thỏa mãn các tính chất
- Tính đóng gói của \\(\mathcal{G}\\) trong phép \\(\otimes\\): \\(\forall x, y \in \mathcal{G}\\) thì \\(x \otimes y \in \mathcal{G}\\).
- Tính kết hợp: \\(\forall x, y, z \in \mathcal{G}\\) thì \\((x \otimes y) \otimes z = x \otimes (y \otimes z)\\).
- Tồn tại phần tử đơn vị: \\(\exists e \in \mathcal{G}, \forall x \in \mathcal{G}\\) thỏa mãn \\(x \otimes e = x\\) và \\(e \otimes x = x\\).
- Tồn tại phần tử nghịch đảo: \\(\forall x \in \mathcal{G}, \exists y \in \mathcal{G}\\) thỏa mãn \\(x \otimes y = e\\) và \\(y \otimes x = e\\).

Nếu nhóm có thêm tính chất giao hoán \\(\forall x, y \in \mathcal{G}: x \otimes y = y \otimes x\\) thì nhóm đó được gọi là nhóm Abelian.

Một nhóm các ma trận khả nghịch \\(A \in \Bbb R^{n \times n}\\) với phép toán nhân ma trận được gọi là một General Linear Group. Tuy nhiên, phép nhân ma trận không có tính chất giao hoán nên nhóm này không phải là một nhóm Abelian. 

#### 2.2. Không gian véc-tơ
Một không gian véc-tơ thực \\(V = (\mathcal{V}, + , \cdot)\\) là một tập \\(V\\) với 2 phép toán
<div style="text-align:center;">

\\(
  +: \mathcal{V} \times \mathcal{V} \to \mathcal{V} \\\\
  \cdot: \Bbb R \times \mathcal{V} \to \mathcal{V}
\\)

</div>

Thỏa mãn
- \\(\mathcal{V}, +\\) là một nhóm Abelian.
- Tính chất phân phối \\(\forall \lambda \in \Bbb R, x, y \in \mathcal{V}: \lambda \cdot(x + y) = \lambda \cdot x  + \lambda \cdot y\\) và \\(\forall \lambda, \psi \in \Bbb R, x \in \mathcal{V}: (\lambda + \psi)\cdot x = \lambda \cdot x + \psi \cdot x\\)
- Tính chất kết hơp \\(\forall \lambda, \psi \in \Bbb R, x \in \mathcal{V}: \lambda \cdot(\psi \cdot x) = (\lambda \cdot \psi)\cdot x\\)
- Tồn tại phần tử đơn vị \\(\forall x \in \mathcal{V}: 1 \cdot x = x\\)

#### 2.3. Không gian véc-tơ con
Với \\(V = (\mathcal{V}, + , \cdot)\\) là một không gian véc-tơ và \\(\mathcal{U} \subseteq \mathcal{V}, \mathcal{U} \ne \emptyset\\) thì \\(U = (\mathcal{U}, + , \cdot)\\) được gọi là không gian véc-tơ con của \\(V\\) nếu \\(U\\) là một không gian véc-tơ cùng với các phép toán \\(+\\) và \\(\cdot\\) ứng với \\(\mathcal{U} \times \mathcal{U}\\) và \\(\Bbb R \times \mathcal{U}\\). Kí hiệu \\(U \subseteq V\\) thể hiện \\(U\\) là một không gian véc-tơ con của \\(V\\).

Nếu \\(U\\) là một không gian véc-tơ con của \\(V\\), \\(U\\) sẽ thừa hưởng tất cả các tính chất của \\(V\\). Để chứng minh \\(U\\) là một không gian véc-tơ con của \\(V\\), chúng ta vẫn phải chỉ ra được
- \\(\mathcal{U} \ne \emptyset\\) hay \\(0 \in \mathcal{U}\\).
- Tính đóng gói của \\(U\\): \\(\forall \lambda \in \Bbb R, \forall x \in \mathcal{U}: \lambda x \in \mathcal{U}\\) và \\(\forall x, y \in \mathcal{U}: x + y \in \mathcal{U}\\).

### 3. Phụ thuộc tuyến tính

#### 3.1. Tổ hợp tuyến tính
Cho một không gian véc-tơ \\(V\\) và một số hữu hạn các véc-tơ \\(\boldsymbol{x_{1}}, \boldsymbol{x_{2}},..., \boldsymbol{x_{k}} \in V\\), mỗi \\(\boldsymbol{v} \in V\\) được biểu diễn dưới dạng

<div style="text-align:center;">

\\(
  \boldsymbol{v} = \lambda_{1}\boldsymbol{x_{1}} + \lambda_{2}\boldsymbol{x_{2}} + ... + \lambda_{k}\boldsymbol{x_{k}} = \sum_{i=1}^{k} \lambda_{i}\boldsymbol{x_{i}} \in V
\\)

</div>

với \\(\lambda_{1}, \lambda_{2},..., \lambda_{k} \in \Bbb R\\), là một tổ hợp tuyến tính của các véc-tơ \\(\boldsymbol{x_{1}}, \boldsymbol{x_{2}},..., \boldsymbol{x_{k}}\\).

Véc-tơ \\(\boldsymbol{0}\\) có thể được viết dưới dạng \\(\boldsymbol{0} = \sum_{i=1}^{k}0x_{i}\\) nhưng chúng ta quan tâm nhiều hơn đến các tổ hợp tuyến tính không tầm thường hơn.

#### 3.2. Phụ thuộc tuyến tính
Nếu có một tổ hợp tuyến tính không tầm thường thỏa mãn \\(0 = \sum_{i=1}^{k} = \lambda_{i}x_{i}\\) với ít nhất một giá trị \\(\lambda_{i} \ne 0\\) thì các véc-tơ \\(\boldsymbol{x_{1}}, \boldsymbol{x_{2}},..., \boldsymbol{x_{k}}\\) được gọi là ***phụ thuộc*** tuyến tính.

Nếu mà biểu thức trên chỉ tồn tại nghiệm tầm thường \\(\lambda_{1} = \lambda_{2} = ... = \lambda_{k}\\) thì các véc-tơ \\(\boldsymbol{x_{1}}, \boldsymbol{x_{2}},..., \boldsymbol{x_{k}}\\) là ***độc lập*** tuyến tính.

Một số tính chất cho các véc-tơ kiểu này là
- \\(k\\) véc-tơ trên hoặc là độc lập tuyến tính, hoặc là phụ thuộc tuyến tính, chứ không có loại khác.
- Nếu ít nhất một trong số các véc-tơ \\(\boldsymbol{x_{1}}, \boldsymbol{x_{2}},..., \boldsymbol{x_{k}}\\) là véc-tơ \\(\boldsymbol{0}\\) thì chúng sẽ phụ thuộc tuyến tính. Tính chất này cũng tương đương với việc có 2 véc-tơ giống nhau trong tập \\(k\\) véc-tơ trên.
- Tập các véc-tơ trên là phụ thuộc tuyến tính nếu như một trong số các véc-tơ đó có thể được biểu diễn dưới dạng tổ hợp tuyến tính của các véc-tơ còn lại.
- Ta viết tất cả véc-tơ thành các cột của một ma trận \\(\boldsymbol{A}\\), sau đó biểu diễn phép khử Gaussian, ta được các pivot columns sẽ độc lập tuyến tính với các véc-tơ ở bên trái của véc-tơ đó, còn các cột không phải pivot columns sẽ có thể được biểu diễn dưới dạng một tổ hợp tuyến tính của các pivot columns ở bên trái của nó. Nếu tất cả các cột đều là pivot columns thì tất cả các véc-tơ đó là độc lập tuyến tính, còn không thì chúng sẽ là phụ thuộc tuyến tính.

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






