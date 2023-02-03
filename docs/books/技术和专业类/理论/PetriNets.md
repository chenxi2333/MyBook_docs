# Petri Nets基础

## Introduction

- 简单介绍和基本特征
  - 定义
  - 特征
  - 用途和历史
- 基本构成
- 运行规则
- Properties of Petri nets
- PN网络分析
  - 线性代数方法
  - 图像分析法
- PetriNets类型
- PetriNets的基本结构
  - Sequence
  - Concurrency and Synchronisation
  - Conflict（Choice）
  - Buffer
  - FIFO queue
  - Machine

## PetriNets的数学描述

- PetriNets的基础构成
  - Def1：结构化N（P,T,F,W）描述网络结构
  - Def2:M表明tokens的分布
- 前件和后件（preset and postset）
  - Def3：x的前件和后件
  - Def4：t的输入和输出place是t的前件和后件
  - Def5：firing的规则和计算
- PN网络的特性：
  - Def6：safe & (un)bounded
  - Def7：pure（self-loop free）即不存在双向的箭头

## PetriNets的矩阵表达

- Def8：用一个矩阵来描述一个pure的网络
  - 状态矩阵[M]
  - 变化矩阵[N]
  - 正半和负半
- Def9：网络的活性
  - live or dead
  - deadlock-free(weakly live)
  - Def10：quasi-live

- Def11：用矩阵表示多次变化并计算变化的结果
  - Def12：legal
  - Def13：legal firing sequence problem
  - 线性化，基于
    - Def14：over the real numbers
    - Def15：over the non-negative integers
    - Def16：using a basis *B* of P-invariants
    - Def17：a basis *Φ* (Phi - pronounced as “faı”) of P-semiflows
    - Theorem1：
    - Def18：consistent 和 conservative
    - Theorem2：





# PetriNets分析

## Structural Invariants

- Def19：P向量和T向量
- Def20：P矩阵和T矩阵
- Def21、22：semiflow
  - Th3\4

## Siphons and Traps

- Def23\24:siphon & Traps
- 



# Petri工具

# INA

