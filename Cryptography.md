# Cryptography 

## Ch1 古典密码

### 凯撒密码

$$
e_k(x)=(x + 3) mod 26\\
d_k(x)=(x - 3) mod 26
$$

### Playfair

(From wikipedia)

1. 选取一个英文字作密鑰。除去重覆出现的字母。将密鑰的字母逐个逐个加入5×5的矩阵内，剩下的空间将未加入的英文字母依a-z的顺序加入。（将Q去除，或将I和J视作同一字。）
2. 将要加密的讯息分成两个一组。若组内的字母相同，将X（或Q）插入两字母之间，重新分组（例如 HELLO 将分成 HE LX LO）。若剩下一个字，也加入X字。
3. 在每组中，找出两个字母在矩阵中的地方。

- 若两个字母不在同一直行或同一橫列，在矩阵中找出另外两个字母，使这四个字母成为一个长方形的四个角。
- 若两个字母在同一橫列，取这两个字母右方的字母（若字母在最右方则取最左方的字母）。
- 若两个字母在同一直行，取这两个字母下方的字母（若字母在最下方则取最上方的字母）。

### Hill密码

$$
y=Kx
$$

K求逆
$$
\left(\begin{array}{cc}a & b \\ c & d\end{array}\right)^{-1}=(a d-b c)^{-1}\left(\begin{array}{cc}d & -b \\ -c & a\end{array}\right)
$$

## 维吉尼亚密码

$$
e_k(x_1, x_2, ..., x_m)=(x_1 + k_1, x_2 + k_2, ...,x_m + k_m)\\
d_k(y_1, y_2, ..., y_m)=(y_1 - k_1, y_2 - k_2, ...,y_m - k_m)
$$



重合指数
$$
I_{c}(x)=\frac{\sum_{i=0}^{25}\left(\begin{array}{c}f_{i} \\ 2\end{array}\right)}{\left(\begin{array}{l}n \\ 2\end{array}\right)} \approx \frac{\sum_{i=0}^{25} f_{i}\left(f_{i}-1\right)}{n(n-1)}
$$
f为频数，n为字符串长度

英语为0.065，随机为0.038

## Ch2 编码与信息论

### 熵

$$
H(x)=-\Sigma_{x\in X}Pr[x]log_2(Pr[x])
$$

###  Huffman编码

## Ch3 分组密码

### AES

### DES

## Ch4 Hash函数



## Ch5 公钥密码

### RSA

举个栗子

$p=47, q=71$

$n=p*q=3337,\phi(n)=(p-1)(q-1)=3220$

随机选取正整数$d=1019,s.t.0<d<3220 \and gcd(d,3220)=1$

计算$e=d^{-1}mod\phi(n)=79$

则`公钥`$e=79,n=3220$, `私钥`$d=1019$

对消息M=668加密，$C=M^{e}mod n= 668^{79}mod3337=1570$

解密：$M=C^{d}mod n = 1570^{1019}mod 3337=668$

