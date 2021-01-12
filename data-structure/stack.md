# 栈

## [判断括号是否合法](https://leetcode-cn.com/problems/valid-parentheses/)

### 方法1，使用栈的方式确认

- 我们对给定的字符串 ss 进行遍历
- 当我们遇到一个左括号时，我们将这个左括号放入栈顶。
- 当我们遇到一个右括号时，我们可以取出栈顶的左括号并判断它们是否是相同类型的括号。
- 如果不是相同的类型，或者栈中并没有左括号，那么字符串 ss 无效，返回False

```golang
func isValid(s string) bool {
    length := len(s)
    if length % 2 == 1 {
        return false
    }

    pairs := map[byte]byte {
        ']' : '[',
        '}' : '{',
        ')' : '(',
    }
    stack := []byte{}

    for i := 0; i < length; i++ {
        char := s[i]
        if c, ok := pairs[char]; ok {
            if len(stack) == 0 || stack[len(stack)-1] != c {
                return false
            }

            stack = stack[:len(stack)-1]
        } else {
            stack = append(stack, char)
        }
    }

    return len(stack) == 0
}
```

### 方法2：替换{}或者[]或者()，知道字符串中不能再替换

```golang
func isValid(s string) bool {
    flag := true
    for flag {
        subflag := false //是否含有{}或者[]或者()

        if strings.Contains(s, "{}"){
            s = strings.ReplaceAll(s, "{}", "")
            subflag = true
        }

        if strings.Contains(s, "[]"){
            s = strings.ReplaceAll(s, "[]", "")
            subflag = true
        }

        if strings.Contains(s, "()"){
            s = strings.ReplaceAll(s, "()", "")
            subflag = true
        }

        if !subflag {
            flag = false
        }
    }

    return len(s) == 0
}
```
