1. 调色盘（Color Palette）,背景色的微调：原版四色（橙绿蓝黄）
2. 形状与细节的微调：
    - 圆角弧度： 原版如果是 4px 圆角，你可以尝试大圆角（更像豆腐，更Q弹）或者超小圆角（更硬朗，更极客）
    - 材质感： 给方块加一点点极其微弱的渐变，或者一点点内阴影，让它看起来像玻璃、像陶瓷或者像塑料积木
3. 消除动画
4. 音效随材质变化，加入ASMR元素
5. 2个候选形状，用掉一个补充一个

- Dreamland
```
const ColorPalette = [
    "", // 0: 无
    "#FF99C8", // 1: 粉
    "#D0F4DE", // 2: 绿
    "#A9DEF9", // 3: 蓝
    "#E4C1F9", // 4: 紫
];
```
- Germany
```
const ColorPalette = [
    "", // 0: 无
    "#F77F00", // 1: 橙
    "#FCBF49", // 2: 金
    "#D62828", // 3: 赤
    "#003049", // 4: 黑
];
```
- France
```
const ColorPalette = [
    "", // 0: 无
    "#88d2ec", // 1: 浅蓝
    "#DA4167", // 2: 红
    "#aa8cc4", // 3: 紫
    "#083d77", // 4: 深蓝
];
"#ebebd3", // 3: 白背景
```
棋盘大小：10x10
方块形状：
```
const SHAPE_CONFIG = [
    // --- 静态组 (SHAPE_LIBRARY_static) ---
    {
        name: "dot",
        matrix: [[1]],
        weight: 10,     
        canRotate: false,
        canMirror: false
    },
    {
        name: "22full",
        matrix: [[1, 1], [1, 1]],
        weight: 60,
        canRotate: false,
        canMirror: false
    },
    {
        name: "5CROSS",
        matrix: [
            [0, 0, 1, 0, 0],
            [0, 0, 1, 0, 0],
            [1, 1, 0, 1, 1],
            [0, 0, 1, 0, 0],
            [0, 0, 1, 0, 0]
        ],
        weight: 5,        
        canRotate: false,
        canMirror: false
    },

    // --- 动态变换组 (SHAPE_LIBRARY) ---
    {
        name: "23L",
        matrix: [[1, 0], [1, 0], [1, 1]],
        weight: 50,
        canRotate: true,
        canMirror: true
    },
    {
        name: "six",
        matrix: [[1, 0], [1, 1], [1, 1]],
        weight: 40,
        canRotate: true,
        canMirror: true
    },
    {
        name: "3dots",
        matrix: [[1, 0], [1, 1]],
        weight: 70,
        canRotate: true,
        canMirror: true
    },
    {
        name: "23Z",
        matrix: [[0, 1, 1], [1, 1, 0]],
        weight: 45,
        canRotate: true,
        canMirror: true
    },
    {
        name: "24Z",
        matrix: [[0, 1], [1, 1], [1, 0], [1, 0]],
        weight: 30,
        canRotate: true,
        canMirror: true
    },
    {
        name: "34Z",
        matrix: [
            [1, 1, 0],
            [0, 1, 0],
            [0, 1, 0],
            [0, 1, 1]
        ],
        weight: 10,      
        canRotate: true,
        canMirror: true
    },
    {
        name: "line2",
        matrix: [[1, 1]],
        weight: 50,
        canRotate: true,
        canMirror: false  
    },
    {
        name: "line3",
        matrix: [[1, 1, 1]],
        weight: 45,
        canRotate: true,
        canMirror: false
    },
    {
        name: "line4",
        matrix: [[1, 1, 1, 1]],
        weight: 15,
        canRotate: true,
        canMirror: false
    },
    {
        name: "line5",
        matrix: [[1, 1, 1, 1, 1]],
        weight: 10,       // 5连长条占地大，设低
        canRotate: true,
        canMirror: false
    },
    {
        name: "stair",
        matrix: [[0, 1, 1], [1, 1, 0], [1, 0, 0]],
        weight: 25,
        canRotate: true,
        canMirror: true
    }
];
```
当游戏需要生成三个新方块时，你的逻辑应该是：

- 随机选型： 从 SHAPE_LIBRARY 里随机挑一个。

- 随机变换： 随机运行 0-3 次 rotateMatrix，或者随机决定是否 mirrorMatrix。

- 上色： 遍历最终生成的矩阵，把 1 变成随机的 ColorID。
```
function rotateMatrix(matrix) {
    // 将行变为列
    return matrix[0].map((_, index) => 
        matrix.map(row => row[index]).reverse()
    );
}

function mirrorMatrix(matrix) {
    return matrix.map(row => [...row].reverse());
}
```
- 提示
- 10元购买去广告
- 排行榜
- 道具兑换（随机颜色单方块）：看广告/分享
- 旋转/翻转功能？
