###1.1.1
算法1是非确定性的，输入到达的顺序决定输出的结果。
算法2是确定性的，对于任意两个输入，输出都是唯一的。
算法1是公平的，即使输入的长度不一样，但是它们都是遵循先到先服务的规则。
算法2是不公平的，每一次都是通过比较两个输入的长度，先取短的，这就有可能会造成长的输入会饿死。
###1.1.2
首先需要定义基础操作
###### a): "+"，两个数相加，in1,in2是输入，out是输出
	for (;;) {
	a := wait(in1);
	b := wait(in2);
	send(a + b, out);
	}
###### b): "*"，两个数相乘，in1,in2是输入，out是输出
	for(; ;){
	a := wait(in1);
	b := wait(in2);
	send(a * b, out);
	}
###### c): "D"，复制，in1是输入，out1,out2是输出
	for(; ; ){
	a := wait(in1);
	send(a, out1);
	send(a, out2);
	}
###### d): "Ci"，常数，in是输入，out是输出，i是常数
	send(i, out);
	for(; ;){
	a := wait(in);
	send(a, out);
	}
######e): "S"：sink 操作将输入in丢弃
	for(; ;){
	wait(in);
	}

f(n) = n(n + 1)/2可以化为： 
f(0) = 0
f(n) = n + f(n − 1), n ≥ 1	
 
计算n:
![enter image description here](https://raw.githubusercontent.com/14353412zzy/ES2016_14353412/master/pictures/1480503434436.jpg)
计算f(n) = n(n + 1)/2:
![enter image description here](https://raw.githubusercontent.com/14353412zzy/ES2016_14353412/master/pictures/IMG_20161130_192139.jpg)

	
###1.2.1
$$
\tag{a}
 \left[
 \begin{matrix}
   1 & -1 \\
   1 & -1
  \end{matrix}
  \right] 
$$
$$
\tag{b}
 \left[
 \begin{matrix}
   2 & -1 \\
   1 & -1
  \end{matrix}
  \right] 
$$
(a)是 consistent，(b)不是
###1.2.2
$$
 \left[
 \begin{matrix}
     1 & -1 & 0 & 0 & 0 & 0\\
     0 & 1 & -1 & 0 & 0 & 0\\
     0 & 0 & 1 & -1 & 0 & 0\\
     0 & 0 & 0 & 1 & -77 & 0\\
     0 & 0 & 0 & 0 & 1 & -1\\
     0 & 0 & 1 & 0 & 0 & -77
  \end{matrix}
  \right] 
$$ 
Therefore it is consistent. 
Fire number: Quelle:77; DCT:77; Q:77; RLC:77; C:1; R:1
