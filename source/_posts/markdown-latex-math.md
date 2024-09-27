---
title: LaTeX - 在Markdown中插入数学公式
date: 2022-05-01 03:50:46
categories: 中文 
tags: 
- Math
---

在Markdown中插入数学公式的语法是 `$数学公式$` 和 `$$数学公式$$`.

## 行内公式

`$2x+3y=34$`

因此,在排版数学公式时,即使没有特殊符号的算式如1+1=2,或者简单的一个字母变量x,也要进入数学模式,使用`$1+1=2$`,`$x$`, 而不是使用排版普通文字的方式. $2x+3y=34$，$1+1=2$， $x$

## 独立公式

独立公式单独占一行,不和其他文字混编  
示例: `$$c=2πr$$  `

## 多行公式

在独立公式中使用\\\\来换行  

```
$$   
2x+3y=34\\   
x+4y=25  
$$
```

$$
2x+3y=34\\   
x+4y=25
$$

## 常用符号

![image-20220501033315739](https://s2.loli.net/2022/05/01/D4PEZjCrWfO56oN.png)

### 上下标 

`$S=a_{1}^2+a_{2}^2+a_{3}^2$`
$$
S=a_{1}^2+a_{2}^2+a_{3}^2
$$

### 括号 

`$f(x, y) = 100 * \lbrace[(x + y) * 3] - 5\rbrace$`
$$
f(x, y) = 100 * \lbrace[(x + y) * 3] - 5\rbrace \\ 
f(x, y) = 100 * \{[(x + y) * 3] - 5\}
$$

### 分数

`$\frac{1}{3} 与 \cfrac{1}{3}$` 
$$
\frac{1}{3} \ 与 \ \cfrac{1}{3}
$$

### 开方

`$\sqrt[3]{X}$` 和 `$\sqrt{5 - x}$`
$$
\sqrt[3]{X} \ 和 \ \sqrt{5 - x}
$$

## 其他字符

### 关系运算符

$$
\pm \ \times \ \div \ \mid \ \nmid \ \cdot \ \circ \ \ast \ \bigodot \ \bigotimes \ \bigoplus \ \leq \ \geq \ \neq \ \approx \ \equiv \ \sum \ \prod
$$

![image-20220501033406229](https://s2.loli.net/2022/05/01/NWYD3vPce9shnHX.png)

### 对数运算符

$$
\log \ \lg \ \ln
$$

![image-20220501033444782](https://s2.loli.net/2022/05/01/YTgwi5HrFhKnxbR.png)

### 三角运算符

$$
\bot \ \angle \ \sin \ \cos \ \tan \ \cot \ \sec \ \csc
$$

![image-20220501033513958](https://s2.loli.net/2022/05/01/vqOX2QVDKsc56xI.png)

### 微积分运算符

$$
\prime \ \int \ \iint \ \iiint \ \oint \ \lim \ \infty \ \nabla \ \mathrm{d}
$$

![image-20220501033539620](https://s2.loli.net/2022/05/01/cs216gjAeQZxnXq.png)

### 集合运算符

$$
\emptyset \ \in \ \notin \ \subset \ \subseteq \ \supseteq \ \bigcap \ \bigcup \ \bigvee \ \bigwedge \ \biguplus \bigsqcup
$$

![image-20220501033612481](https://s2.loli.net/2022/05/01/geXdC9TV7sk5Ij2.png)

### 希腊字母

$$
A \  \alpha \ B \  \beta \  \Gamma \  \gamma \ \\
\Delta \  \delta \ E \  \epsilon \ Z \  \zeta \ \\
H \  \eta \  \Theta \  \theta \ I \  \iota \ \\
K \  \kappa \ \Lambda \  \lambda \ M \  \mu \ N \  \nu \ \\
Xi \  \xi \ O \  \omicron \  \Pi \  \pi \ \\
P \  \rho \  \Sigma \  \sigma \ T \  \tau \ \\
 \Upsilon \  \upsilon \  \Phi \  \phi \ \\
 X \  \chi \  \Psi \  \psi \  \Omega \  \omega
$$

![image-20220501034204219](https://s2.loli.net/2022/05/01/42K15g7sFchql3S.png)
