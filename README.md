# 贪心算法
> 贪心算法的本质就是局部最优推导出全局最优，是一种在每一步选择中都采取在当前看来是最好的选择，不从整体上对问题进行分析，从局部出发，通过不断寻找问题的最优解来解决整体问题的方法。

## 贪心算法的应用场景
1. 分发饼干

    假设你是一位很棒的家长，想要给你的孩子们一些小饼干。但是，每个孩子最多只能给一块饼干。
    
    对每个孩子i，都有一个胃口值g[i]，这是能让孩子们满足胃口的饼干的最小尺寸；并且每块饼干 j，都有一个尺寸 s[j]。如果 s[j]>=g[i]，我们可以将这个饼干 j 分配给孩子 i ，这个孩子会得到满足。你的目标是尽可能满足越多数量的孩子，并输出这个最大数值。

    [] 解释：
    局部最优解是大饼干喂给胃口大的小孩，全局最优就是喂饱尽可能多的小孩。

    [] 解题思路：
    可以尝试使用贪心策略，先将饼干数组和小孩数组排序。然后从后向前遍历小孩数组，用大饼干优先满足胃口大的，并统计满足小孩的数量。

2. 摆动序列

    如果连续数字之间的差严格地在正数和负数之间交替，则数字序列称为摆动序列。第一个差（如果存在的话）可能是正数或负数。少于两个元素的序列也是摆动序列。例如， [1,7,4,9,2,5] 是一个摆动序列，因为差值 (6,-3,5,-7,3)  是正负交替出现的。相反, [1,4,7,2,5]  和  [1,7,4,5,5] 不是摆动序列，第一个序列是因为它的前两个差值都是正数，第二个序列是因为它的最后一个差值为零。给定一个整数序列，返回作为摆动序列的最长子序列的长度。 通过从原始序列中删除一些（也可以不删除）元素来获得子序列，剩下的元素保持其原始顺序。

    [] 解释：
    最优解其实就是获取最多的局部峰值，那么局部最优就是删除单调坡度上的节点(不包括单调坡度两端的节点)，那么这个坡度就可以有两个局部峰值。
    
    [] 解题思路：

    1) 上下坡中有平坡
    2) 数组首尾两端
    3) 单调坡中有平坡

3. 最大子序和

    给定一个整数数组nums,找到一个具有最大和的连续子数组(子数组最少包含一个元素)，返回其最大和

    [] 解释:
    局部最优：当前连续和为负数的时候立刻放弃，从下一个元素重新计算连续和，因为负数加上下一个元素连续和只会越来越小。全局最优：选取最大连续和。

    [] 解题思路:

    很简单的想法就是只要前面相加为负数了，就从0开始，前面所有全都放弃。并且要让前面的结果和当前的结果作比较得出最大值

4. 买卖股票的最佳时机

    给定一个数组，它的第  i 个元素是一支给定股票第 i 天的价格。设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

    [] 解释：局部最优是相减是正值，得到全局正值

    [] 解题思路：只收集有正利润的时候就是贪心

5. 跳跃游戏

    给定一个非负整数数组，你最初位于数组的第一个位置。数组中的每个元素代表你在该位置可以跳跃的最大长度。判断你是否能够到达最后一个位置。

    [] 解释:
        在每一个区间里寻找下一步的最大步数，就是全局的最大步数
    
    [] 重要的知识点:
        
        这里有一个重要的知识点，对于js来说，let是可变量，那么在for循环的时候如果使用了let的变量在for循环之后才会销毁，也就是说，在for里面重新给这个变量赋值，这个for循环就会持续进行，直到这个变量不再改变为止，或者return 为止。

        `
            function func(arr) {
                let current = 0;
                for (let i = 0; i <= current; i++) {
                    current = Math.max(arr[i] + i, current); // 持续变长
                    if (current >= arr.length - 1) return true;
                }
                return false;
            }
        `
6. 跳跃游戏 II

    给定一个非负整数数组，你最初位于数组的第一个位置。数组中的每个元素代表你在该位置可以跳跃的最大长度。你的目标是使用最少的跳跃次数到达数组的最后一个位置。

    []解释：局部最优解就是当前范围里(就是i === curentIndex)，找到下一步的最大值，然后步数加一，并且把当前的范围改成这个下一步的最大值(curIndex = nextIndex)。注意的点就是这里改变的是索引，数组里的值也是索引所以就有了max(num[i] + i, nextIndex)

    []解题思路： 以最小的步数，增加最大的覆盖范围，直到覆盖范围覆盖了终点，这个范围内最少步数一定可以跳到，不用管具体是怎么跳的，不纠结于一步究竟跳到一个单位还是两个单位。

7. K次取反后最大化的数组和

    给定一个整数数组 A，我们只能用以下方法修改该数组：我们选择某个索引 i 并将 A[i] 替换为 -A[i]，然后总共重复这个过程 K 次。（我们可以多次选择同一个索引 i。）以这种方式修改数组后，返回数组可能的最大和。

    []解释：首先要先把所有的负值都变成正值；那么如果将负数都转变为正数了，K依然大于0，此时的问题是一个有序正整数序列，如何转变K次正负，让 数组和 达到最大。这又是另外一个贪心，将所有的正数从大到小排列，然后更改小的值
    1) 先将所有负值都变为正数
    2) 如果key还有，那就将最小的正值变为负数
    3) 全部都是负数，且所有都遍历一遍之后，key还是有剩下的

    []解题思路：最大和其实是关键,不需要管次序只需要最大和就好。其中比较重要的点是，之前加上的值，后面要记的减两遍。

8. 加油站

    在一条环路上有 N 个加油站，其中第 i 个加油站有汽油 gas[i] 升。你有一辆油箱容量无限的的汽车，从第 i 个加油站开往第 i+1 个加油站需要消耗汽油 cost[i] 升。你从其中的一个加油站出发，开始时油箱为空。如果你可以绕环路行驶一周，则返回出发时加油站的编号，否则返回 -1。

    []解释: 

        本地的重点就是是否能走完一圈，也就是确定行驶站点开始之后，
        `
            let currentCost = 0; // 当前油箱剩余的油量
            let c = 0; // 站点
            for (let i = 0; i < gas.length; i++) {
                currentCost += gas[i] - cost[i];
                if (currentCost < 0) {
                    c = i + 1;
                    currentCost = 0;
                }
            }
        `
        走一圈，再看油箱的油量是不是大于0，
        `
            for (let i = 0; i < c; i++) {
                currentCost += gas[i] - cost[i];
            }

        `
        就能判断出来是否走完一圈了。如果能走完返回行驶站点就可以。

        `
            if (currentCost < 0) return -1;
            return c;
        `

    []解题思路: 
        1) 加油站的两个相隔的汽油差，减去需要的汽油差，如果油箱剩余的汽油量小于0，到i为止，就是从i开始出发，然后遍历到一圈为止。看油箱剩余的汽油量，小于零就返回-1，否则返回i。

9. 分发糖果

    老师想给孩子们分发糖果，有 N 个孩子站成了一条直线，老师会根据每个孩子的表现，预先给他们评分。你需要按照以下要求，帮助老师给这些孩子分发糖果：每个孩子至少分配到 1 个糖果。相邻的孩子中，评分高的孩子必须获得更多的糖果。那么这样下来，老师至少需要准备多少颗糖果呢？

    []解释 

    这题第一步确定两次贪心，第二步就是要确定，从那一侧开始遍历。

    先给右侧最多的孩子时，因为要依赖前面孩子的糖的数量，所以要从左往右遍历。同理可得，给左侧最多的孩子遍历时，从右往左遍历。因为已经做过一次赋值了，所以第二次要判断小值加一和当前值谁大。

    []解题思路 假设每一个人都先有一棵糖，分别从两侧，先给所有右侧更多的孩子分发，再给所有左侧最多的孩子分发

10. 柠檬水找零

    在柠檬水摊上，每一杯柠檬水的售价为 5 美元。顾客排队购买你的产品，（按账单 bills 支付的顺序）一次购买一杯。每位顾客只买一杯柠檬水，然后向你付 5 美元、10 美元或 20 美元。你必须给每个顾客正确找零，也就是说净交易是每位顾客向你支付 5 美元。注意，一开始你手头没有任何零钱。如果你能给每位顾客正确找零，返回 true ，否则返回 false 。

    []解释

    这里要注意的是，在判断里一旦5元或者10元的数量小于0，就返回false。不然累加不会出现一直为true的情况。


    []解题思路: 

     1) 5元就存下
     2）10元优先给5元 5
     3) 20元优先给10元 10+5 5+5+5 

11. 根据身高重建队列

    假设有打乱顺序的一群人站成一个队列，数组 people 表示队列中一些人的属性（不一定按顺序）。每个 people[i] = [hi, ki] 表示第 i 个人的身高为 hi ，前面 正好 有 ki 个身高大于或等于 hi 的人。请你重新构造并返回输入数组 people 所表示的队列。返回的队列应该格式化为数组 queue ，其中 queue[j] = [hj, kj] 是队列中第 j 个人的属性（queue[0] 是排在队列前面的人）。

    []解释 

    [[7,0],[4,4],[7,1],[5,0],[6,1],[5,2]]


    []解题思路 本题有两个维度，遇到这种题目一定要想如何确定一个维度，然后再按照另一个维度重新排列。与分发糖果的题类似。

    > 遇到两个维度权衡的时候，一定要先确定一个维度，再确定另一个维度。如果两个维度一起考虑一定会顾此失彼。
    
    本题主要是要确定第一个维度，是h还是k，因为是按照身高排序所以选择身高。按照身高排序之后，优先按身高高的people的k来插入，后序插入节点也不会影响前面已经插入的节点，最终按照k的规则完成了队列。

    排序之后
    局部最优：优先按身高高的people的k来插入。插入操作过后的people满足队列属性

    全局最优：最后都做完插入操作，整个队列满足题目队列属性

12. 用最少数量的箭引爆气球

    在二维空间中有许多球形的气球。对于每个气球，提供的输入是水平方向上，气球直径的开始和结束坐标。由于它是水平的，所以纵坐标并不重要，因此只要知道开始和结束的横坐标就足够了。开始坐标总是小于结束坐标。一支弓箭可以沿着 x 轴从不同点完全垂直地射出。在坐标 x 处射出一支箭，若有一个气球的直径的开始和结束坐标为 xstart，xend， 且满足  xstart ≤ x ≤ xend，则该气球会被引爆。可以射出的弓箭的数量没有限制。 弓箭一旦被射出之后，可以无限地前进。我们想找到使得所有气球全部被引爆，所需的弓箭的最小数量。给你一个数组 points ，其中 points [i] = [xstart,xend] ，返回引爆所有气球所必须射出的最小弓箭数。

    [] 解释


    [] 解题思路

    ******************************************* 有疑惑



13. 无重叠区间

    给定一个区间的集合，找到需要移除区间的最小数量，使剩余区间互不重叠。注意: 可以认为区间的终点总是大于它的起点。 区间 [1,2] 和 [2,3] 的边界相互“接触”，但没有相互重叠。

    []解释 重点是没有相互重叠。 重点是让每一个区间的最大值，都与上一个区间的最大值保持最远距离

    []解题思路

    重叠区域，此类问题，排序都是必要的。

    另外一个比较重要的要确定的问题是，排序的方向从左至右还是从右到左，正向还是逆向，要以谁为基准排序

    本题的关键在于，先以最大值为基础排序，排序之后，的重点就在于，每个区间的贪心策略就是找到覆盖大的值多的区间或者覆盖值数量少的区间，并且保留，然后跟下一个区间进行比较。这样保证了，每一个当前区间都都尽可能的离上一个区间远
    
    `
    代码片段

        points.sort((a, b) => b[1] - a[1]); 
        let num = 0;
        for(let i = 1; i < points.length; i ++) {
            if (points[i][1] > points[i - 1][0]) {
                num ++;
                if (points[i][0] < points[i - 1][0]) {
                    points[i][0] = points[i - 1][0];
                }
            }
        }
        return num;
    `

14. 划分字母区间 abcabc

    字符串 S 由小写字母组成。我们要把这个字符串划分为尽可能多的片段，同一字母最多出现在一个片段中。返回一个表示每个字符串片段的长度的列表。

    []解释

    []解题思路

    统计每一个字符最后出现的位置;
    
    从头遍历字符，并更新字符的最远出现下标，如果找到字符最远出现位置下标和当前下标相等了，则找到了分割点

15. 给出一个区间的集合，请合并所有重叠的区间。

    []解释

    这种集合覆盖问题，一看又是要先排序，那么就先确定维度。因为考虑到重叠的区域最大，所以维度选择左侧值，

    []解题思路

    主要是要考虑清楚判断条件，当 当前值的最小值比前一个最大值大的时候，说明没有重叠，那么就push上一个值，否则就更新最大值。

    `

        let cur = points[i];
        if (cur[0] > prev[1]) {
        arr.push(prev);
        prev = cur;
        } else {
        prev[1] = Math.max(prev[1], cur[1]);
        }
    `


16. 单调递增的数字

    给定一个非负整数 N，找出小于或等于 N 的最大的整数，同时这个整数需要满足其各个位数上的数字是单调递增。（当且仅当每个相邻位数上的数字 x 和 y 满足 x <= y 时，我们称这个整数是单调递增的。）

    []解释 

    输入: N = 332
    输出: 299

    []解题思路

    从后往前遍历，右边比左边大就过，反之，就为9，并且把这个后面的值都改成9(保存改为9的位置)，然后左侧-1，最后得到的数据就是当前的数值加上所有的9


# 动态规划

# 回溯算法

> 回溯法也可以叫做回溯搜索法，它是一种搜索的方式。在二叉树系列中，我们已经不止一次，提到了回溯，例如二叉树：以为使用了递归，其实还隐藏着回溯 (opens new window)。回溯是递归的副产品，只要有递归就会有回溯。

> 回溯的本质是穷举，穷举所有可能，然后选出我们想要的答案。也就是暴力搜索，性能很差

`

    回溯法使用场景

    组合问题：N个数里面按一定规则找出k个数的集合

    切割问题：一个字符串按一定规则有几种切割方式

    子集问题：一个N个数的集合里有多少符合条件的子集

    排列问题：N个数按一定规则全排列，有几种排列方式

    棋盘问题：N皇后，解数独等等

`
## 回溯和递归的区别
递归是一种算法结构，递归会出现在子程序中，形式上表现为直接或间接的自己调用自己。而回溯是一种算法思想，它是用递归实现的回溯的过程类似于穷举法，但回溯有剪纸功能，即自我判断过程。<br />
我们在路上走着，前面是一个多岔路口，因为我们并不知道应该走哪条路，所以我们需要尝试。尝试的过程就是一个函数。
如果我们选择了一个方向，后来发现又有一个多岔路口，这时候又需要进行一次选择。所以我们需要在上一次尝试结果的基础上，再做一次尝试，即在函数内部再调用一次函数，这就是递归的过程。
这样重复了若干次之后，发现这次选择的这条路走不通，这时候我们知道我们上一个路口选错了，所以我们要回到上一个路口重新选择其他路，这就是回溯的思想。


## 回溯法模板
~ 回溯函数模板返回值以及参数
<br />
~ 回溯函数终止条件
<br />
~ 回溯搜索的遍历过程
<br />

`

    void backtracking(参数) {
        if (终止条件) {
            存放结果;
            return;
        }
        for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
            处理节点;
            backtracking(路径，选择列表); // 递归
            回溯，撤销处理结果
        }
    }
`

## 回溯法具体题目

1. 组合

    给定两个整数 n 和 k，返回 1 ... n 中所有可能的 k 个数的组合。示例: 输入: n = 4, k = 2 输出: [ [2,4], [3,4], [2,3], [1,2], [1,3], [1,4], ]

    []解释

    回溯法的搜索过程就是一个树形结构的遍历过程，可以用for循环用来横向遍历，递归的过程事纵向遍历。

    []解题思路

    一般要画出一个递归树，然后用递归写代码。

    从左向右取数，取过的数不在重复取：
    取1： 在1,2,3 中取一个数
    取2： 在3，4中取一个数
    取3： 在4中取一个数
    取4： 空

    `

        const combineHelper = (n ,k, startIndex) => {
            if (path.length === k) {
                result.push([...path])
                return
            }
            for (let i = startIndex; i <= n; i++) { 
                path.push(i); // -> [1, ] 横向
                combineHelper(n ,k, i + 1); // -> [1, 2], [1, 3], [1, 4] 纵向
                path.pop();
            }
        }

    `
    [] 剪枝优化

    `
        const combineHelper = (n ,k, startIndex) => {
            if (path.length === k) {
                result.push([...path])
                return
            }
            for (let i = startIndex; i <= n - (k - path.length) + 1; i++) {
                path.push(i);
                combineHelper(n ,k, i + 1);
                path.pop();
            }
        }
    `

2. 组合总和

    找出所有相加之和为 n 的 k 个数的组合。组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。

    []解释

    []解题思路

# 递归

# 排序

# 二分查找

# 双指针

# 图论

# 字符串

# 链表

# 树

# 堆

# 并查集

