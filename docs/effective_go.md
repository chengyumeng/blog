# 如何优雅地编写 Go 语言代码（一）？

在过去很久，我一直收集优秀的 Go 语言书写规范，因为我一直认为:

```
如果说优雅也有缺点的话，那就是你需要艰巨的工作才能得到它，需要良好的教育才能欣赏它。
```

这句话是伟大的迪杰斯克拉说的。

本文会作为编程规范三部曲的第一部分，主要介绍下面的相关内容：
- 注释
- 命名规范

## 注释

一切公共函数和变量都要有注释，这是无可争辩的，同时，公共函数和变量的注释应该以函数名或者变量名为第一个单词（词汇），例如：

```go
// Request represents a request to run a command.
type Request struct { ...

// Encode writes the JSON encoding of req to w.
func Encode(w io.Writer, req *Request) { ...
```

每一个包都应该有注释，遵循 godoc 的约定，包的注释应该在package xxx 这一行的前面，并且不应该存在空行。对于普通的 package，注释的开端应该使用这样的句式：package xxx，例如：

```go
// Package math provides basic constants and mathematical functions.
package math
```
相比较而言，main 函数会有一些差别，通常而言，他们会以编译后二进制文件的名字来作为注释开端的一部分，假设二进制文件名字为 seedgen ，他们一般采用如下方式声明注释：

```go
// Binary seedgen ...
package main
```

```go
// Command seedgen ...
package main
```

```go
// Program seedgen ...
package main
```

```go
// The seedgen command ...
package main
```

```go
// The seedgen program ...
package main
```

```go
// Seedgen ...
package main
```

需要解释一下的是，在 Go 官方推荐的写法中，一般而言都采用 C++ 风格的注释，也就是上面介绍过的 ”// xxx“ 这种类型，只有一种情况建议采用 C 风格的注释，也就是 ”/* */“ 这种，那就是很多行，很复杂的注释内容，例如：

```go
/*
Package regexp implements a simple library for regular expressions.

The syntax of the regular expressions accepted is:

    regexp:
        concatenation { '|' concatenation }
    concatenation:
        { closure }
    closure:
        term [ '*' | '+' | '?' ]
    term:
        '^'
        '$'
        '.'
        character
        '[' [ '^' ] character-ranges ']'
        '(' regexp ')'
*/
package regexp
```

在有些时候，我们会给一组变量提供公共的注释，例如：

```go
// Error codes returned by failures to parse an expression.
var (
    ErrInternal      = errors.New("regexp: internal error")
    ErrUnmatchedLpar = errors.New("regexp: unmatched '('")
    ErrUnmatchedRpar = errors.New("regexp: unmatched ')'")
    ...
)
```

在这种情况下，并不建议对每一个变量单独注释。

## 命名规范



