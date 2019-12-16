# 编译原理

[TOC]

## 语法分析

### Top-Down Parsers

#### LL(1)文法

1. [FIRST & FOLLOW](https://www.youtube.com/watch?v=N9UuAPU6DAg&list=PLEbnTDJUr_IcPtUXFy2b1sGRPsLFMghhS&index=5)
2. [LL(1)预测分析表](https://www.youtube.com/watch?v=R1ZlWEZWMKk&list=PLEbnTDJUr_IcPtUXFy2b1sGRPsLFMghhS&index=7)
3. 消除左递归
4. 提取左公因子

#### LL(k)文法

- 给定k>0, 一个CFG是否为LL(k) 文法是可判定的 

- 对于一个CFG, 是否存在k>0, 使得该文法是LL(k) 文法, 是不可判定的 

- 两个LL(k) 文法的语言是否相等是可判定的 
- LL(k) 文法是无二义文法 

- LL(k) 文法中不存在左递归的非终结符 

- 给定k>0, 不含$\epsilon$产生式的 LL(k) 文法的语言类严格包含于不含$\epsilon$产生式的 LL(k+1) 文法的语言类 

### Bottom-Up Parsers

#### LR(0)分析

1. [LR(0) items and LR(0) parsing table](https://www.youtube.com/watch?v=APJ_Eh60Qwo&list=PLEbnTDJUr_IcPtUXFy2b1sGRPsLFMghhS&index=10)
2. [LR(0) parsing](https://www.youtube.com/watch?v=0kiTNN2kHyY&list=PLEbnTDJUr_IcPtUXFy2b1sGRPsLFMghhS&index=11)

