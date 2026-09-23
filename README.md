# AVLForge — AVL 树锻造炉

<p align="center">
  <a href="https://github.com/CJX0712/avl-forge/actions/workflows/ci.yml"><img src="https://github.com/CJX0712/avl-forge/actions/workflows/ci.yml/badge.svg" alt="ci"></a>
  <a href="https://github.com/CJX0712/avl-forge/releases"><img src="https://img.shields.io/github/v/release/CJX0712/avl-forge?sort=semver" alt="release"></a>
  <a href="https://github.com/CJX0712/avl-forge/blob/main/LICENSE"><img src="https://img.shields.io/github/license/CJX0712/avl-forge" alt="license"></a>
  <img src="https://img.shields.io/badge/author-%E6%99%A8%E6%98%9F-1f6feb" alt="author">
</p>

单文件离线 AVL 自平衡二叉搜索树工作台。零依赖、离线可用、浏览器直接打开。

## 能干什么

- **插入 / 删除**：实时重绘树形，节点颜色编码平衡因子（绿 bf=0 / 黄 bf=±1 / 红 |bf|>1——若出现即 bug）
- **随机批量**：一键 50 插入 / 20 删除，看旋转如何自动维持平衡
- **中序布局**：x 坐标 = 中序序号，y = 深度—— BST 有序性直接可视化
- **内置自检**：结构不变量 + 经典旋转形状 + 高度上界，随时重跑

1962 年 Adelson-Velsky & Landis 的经典结构：任意操作后每节点左右子树高度差 ≤ 1。

## 无头验证（Node，8/8 全绿）

1. **500 随机操作，每操作后全树校验**：BST 有序（递归上下界）、bf∈{-1,0,1}、存储高度=实际高度、存储大小=实际大小、中序遍历 == JS `sort` 参照数组
2. **AVL 高度上界定理**：n=100..10000，h ≤ 1.4405·log₂(n+2) − 0.328
3. **最坏情况有序插入**：1..4095 升序/降序 → 完美树 h=12（BST 退化为链表 h=4094 的场景，AVL 保持对数）
4. 四种旋转形状：LL/RR/LR/RL 经典序列 → 根全为 2
5. 集合语义：重复插入忽略、成员关系与 Set 参照全量一致（含半量删除后）
6. 空树删除 / 删除不存在值 = 无副作用
7. 确定性
8. 2000 混合操作每 100 步设检查点，不变量全程存活

```bash
node _smoke.js   # 8/8
node _probe.js   # ASCII 树形 dump：LL 旋转 / 经典多旋 / 完美树 / 根删除
```

## 数学注脚

- 高度上界：h < 1.4405·log₂(n+2) − 0.3277（Fibonacci 树是最坏情况）
- 插入只需**一次**旋转（在最低失衡点）；删除可能 O(log n) 次旋转
- 1..4095 升序插入恰好得到完美树（h = log₂(4096) − 1 = 12）

## 用法

浏览器打开 `index.html` 即可。输入数值 → 插入/删除，或批量随机操作；自检面板随时重跑核心断言。

## License

MIT
