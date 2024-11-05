#  Golang学习笔记

没有哪些内容：

1、没有类
2、没有方法重载
3、没有继承
4、没有枚举类型
5、没有try/catch
6、没有泛型



对整型数组排序：`sort.Ints(nums)`、`slices.Sort(nums)`
二分查找：`sort.SearchInts(nums, target)`---表示找到第一个大于等于target的下标，返回值能是len(nums)
数组的定义：`prefix, ans := make([]int, n+1), make([]int, n)`分别定义prefix数组和ans数组，长度分别为n+1和n
切片：`a=nums[:i+1]`a表示以nums[i]结尾的所有子数组。
定义最大值和最小值：math.MaxInt和math.MinInt



523.连续的子数组和

```cpp
func checkSubarraySum(nums []int, k int) bool {
    hash := make(map[int]int)//定义哈希表并初始化
    hash[0] = -1
    //hash := map[int]int{0 : -1}//这样也可初始化
    sum := 0
    for i, num := range nums {
        sum += num
        t := (sum%k+k)%k
        if index, has := hash[t]; has {
            if i-index >= 2 {
                return true;
            }
        } else {
            hash[t] = i
        }
    }
    return false

}
```

哈希表的定义：`hash := make(map[int]int)或者hash := map[int]int{初始化列表 key : value}`
if,else的写法很严格，else一定要在if结尾的}之后，其它地方都不行
当你声明了一个变量的时候，如果这个代码范围中没有用到这个变量会报错declared and not used
`if index, has := hash[t]; has {...}`这里是在if语句中定义index由hash[t]赋值和has为bool类型(存在hash[t]为true,否则为false),然后依据has的真假判断是否进入循环





437.路径总和

```cpp
func pathSum(root *TreeNode, targetSum int) int {
    ans := 0
    hash := make(map[int]int)
    hash[0] = 1
    var dfs func(*TreeNode, int)//声明dfs函数
    dfs = func(node *TreeNode, sum int) {
        if node == nil {
            return
        }
        sum += node.Val
        ans += hash[sum-targetSum]
        hash[sum]++
        dfs(node.Left, sum)
        dfs(node.Right, sum)
        hash[sum]--
    }
    dfs(root, 0)
    return ans
}
```

`var dfs func(*TreeNode, int)`Go能在函数里面写函数，但是需要提前声明一下，这里的声明可以只写参数类型就行，不同于C++的指针类型，在Go语言中 * 号要打在变量的前面而不是后面，比如这里的`root *TreeNode `，然后就是判空，空指针的符号是`nil`而不是`nullptr`，然后就是要获取指针类型里面的数据不是通过`->`来指出的，而是用`.`的方式指出比如`node.Val`





对二维数组的使用：

```go
//二维dp数组的定义
n := len(s)
dp := make([][]int, n)

//对二维数组的遍历操作
for i := range dp {
    dp[i] = make([]int, n)//这一步操作一定要写，不写报错。。。
}
for i := 0; i < n; i++ {
    for j := 0; j < n; j++ {
        dp[i][j] = -1
    }
}

//这是一个记忆化搜索的例子516.最长回文子序列
var dfs func(int, int) int//函数声明 var 函数名 func(参数类型) 返回值类型

//这里在返回值类型的地方顺便定义了res，对后面赋值有作用
dfs = func(i, j int) (res int) {
    if i > j {
        return 0
    }
    if i == j {
        return 1
    }
    
    //定义一个p指针指向visited数组
    p := &visited[i][j]
    
    //记忆化搜索 出现过就返回
    if *p != -1 {
        return *p
    }
    //go中不能有return visited[i][j] = dfs(i+1, j-1)+2的操作 这也是为什么定义指针p和延迟函数
    //延迟函数执行 在函数返回之前先将res的值赋值给*p也就是赋值给visited[i][j]
    defer func() {
        *p = res
    }()
    if(s[i] == s[j]) {
        return dfs(i+1,j-1)+2
    }
    return max(dfs(i+1, j), dfs(i, j-1))
}
return dfs(0, n-1)

```



对字符串的使用：

```go
func smallestBeautifulString(s string, k int) string {
    limit := 'a' + byte(k)
    str := []byte(s)
    n := len(str)
    i := n-1
    str[i]++
    for i < n {
        if str[i] == limit {
            if i == 0 {
                return ""
            }
            str[i] = 'a'
            i--
            str[i]++
        } else if (i > 0 && str[i] == str[i-1]) || (i > 1 && str[i] == str[i-2]) {
            str[i]++
        } else {
            i++
        }
    }
    return string(str)
}
```

go无法对字符串直接修改，只能先转化成byte字节数组类型，字节数组可以和C++的string一样实现字符串的修改操作，limite一定要转化成byte类型，只有同类型的数据才能进行逻辑运算



- go没有三目运算符





##  单调栈+循环数组

```go
func nextGreaterElements(nums []int) []int {
    n := len(nums)
    ans := make([]int, n)
    for i := range ans {
        ans[i] = -1
    }

    st := []int{}
    for i := 0; i < 2*n; i++ {
        x := nums[i%n]
        for len(st) > 0 && x > nums[st[len(st)-1]] {
            ans[st[len(st)-1]] = x
            st = st[:len(st)-1]
        }
        if i < n {
            st = append(st, i)
        }
    }
    return ans
}
```



##  二维数组遍历

```go
func minimumArea(grid [][]int) int {
    up, left, down, right := 1001, 1001, -1, -1
    for i, row := range grid {
        for j, x := range row {
            if x == 1 {
                up = min(up, i);
                left = min(left, j);
                down = max(down, i);
                right = max(right, j);
            }
        }
    }
    return (right-left+1) * (down-up+1)
}
```





##  哈希表

```go
func containsNearbyDuplicate(nums []int, k int) bool {
    hash := make(map[int]int)//nums[i] -- i
    for i, x := range nums {
        if j, ok := hash[x]; ok && i-j <= k {
            return true;
        }
        hash[x] = i
    }
    return false;
}
```

像for里面一样，if里面也能写定义，哈希表的参数定义相较于数组要少一个range





##  切片、二分查找

```go
func countSubarrays(nums []int, k int) int64 {
    ans := 0
    for i, x := range nums {
        for j := i-1; j >= 0 && (x&nums[j] != nums[j]); j-- {
            nums[j] &= x;
        }

        a := nums[:i+1]
        ans += sort.SearchInts(a, k+1) - sort.SearchInts(a, k)
    }
    return int64(ans)
}
```

切片a表示nums数组前i+1个元素，也就是以nums[i]结尾的所有子数组。go语言内置的二分查找函数为sort.SearchInts(array, target);其返回值是int类型的在类型转换的时候需要留意一下。



## 实现dfs

```go
func pathSum(root *TreeNode, targetSum int) (ans [][]int) {
    path := []int{}
    var dfs func(*TreeNode, int)
    dfs = func(node *TreeNode, left int) {
        if node == nil {
            return
        }
        left -= node.Val
        path = append(path, node.Val)
        //它的作用是将 path 切片的最后一个元素删除，也就是恢复 path 在进入当前节点之前的状态。defer是一个延迟函数
        defer func() {path = path[:len(path)-1]}()
        if node.Left == node.Right && left == 0 {
            //来创建一个新的切片并将 path 的内容复制进去，然后再添加到 ans 中，这样做是为了避免后续对 path 的修改影响到已经添加到 ans 中的结果
            ans = append(ans, append([]int{}, path...))
            return
        }
        dfs(node.Left, left)
        dfs(node.Right, left)
        //path = path[:len(path)-1]
    }
    dfs(root, targetSum)
    return
}
```



