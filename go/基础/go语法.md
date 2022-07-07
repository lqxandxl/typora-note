# 基础

## 变量的声明

变量的声明是go的独有内容。go语言其实没有必要写分号，换行就等于分号了。

```
//注意，这只是声明 age为int类型
var age int;
```

## 变量分类

分为几种，数字，布尔（bool），字符串（string），以及派生类型。派生类型比较复杂。

go在声明变量的时候，可以一次为多个变量声明类型。

go的声明和c不同的是，声明之后还是有变量的，只不过是零值。

```
//声明
var identifier1, identifier2 type
//声明+初始化
var a = "liqixin"

//派生类有以下几种声明方式
var a *int
var a []int
var a map[string] int //暂略
var a chan int //暂略
var a func(string) int
var a error // error 是接口

//简略写法
intval := 1 相当于：
var intval int
intval = 1

//多变量赋值
vname1, vname2, vname3 := v1, v2, v3 // 出现在 := 左侧的变量不应该是已经被声明过的，否则会导致编译错误

//因式分解声明
var (
    vname1 v_type1
    vname2 v_type2
)
```

int、float、bool 和 string 这些基本类型都属于值类型。另外go语言不允许连续声明。

## 常量

常量分为显式和隐式。

```
//显式
const b string = "abc"
//隐式
const b = "abc"
//简单写法
const(
	a=11
	b=22
	c=33
)
//枚举 iota自动累加
const (
  a = iota   //0
  b          //1
  c          //2
  d = "ha"   //独立值，iota += 1
  e          //"ha"   iota += 1
  f = 100    //iota +=1
  g          //100  iota +=1
  h = iota   //7,恢复计数
  i          //8
)
```



## 判断语句的写法

```
if 这里不带括号了 {
	//code
}
else if {
	//code
}
else{
	//code
}
```

## 循环语句

循环语句和c相比少了括号

```
//基本的for
for init; condition; post { }
//while
for condition {}
//对于map，数组，slice，字符串循环，key、value可以根据需要写
for key, value := range oldMap {
    newMap[key] = value
}
//如果只想读value
for _, value := range oldMap
```

## 函数

```
//普通函数的写法
func swap(x, y string) (string, string) {
   return y, x
}
```

### 函数闭包：

定义：

当一个函数的返回值是另外一个函数，而返回的那个函数如果调用了其父函数内部的其它变量，如果返回的这个函数在外部被执行，就产生了闭包。

表现形式：

使父亲函数外部能够调用父亲函数内部定义的变量。

理解：

其实如何理解闭包这个概念需要更简洁的方式。定义如下：

只要是个函数，引用了非当前scope的变量，就立刻成为了closure。但是不同的人认为，这样还不足以形成闭包，必须是出现上述的表现形式才算形成了闭包。

```
package main

import "fmt"

//getSequence函数返回了一个函数
func getSequence() func() int {
   i:=0
   return func() int {
      i+=1
     return i  
   }
}

func main(){
   /* nextNumber 为一个函数，函数 i 为 0 */
   nextNumber := getSequence()  

   /* 调用 nextNumber 函数，i 变量自增 1 并返回 */
   fmt.Println(nextNumber()) //1
   fmt.Println(nextNumber()) //2
   fmt.Println(nextNumber()) //3
   
   /* 创建新的函数 nextNumber1，并查看结果 */
   nextNumber1 := getSequence()  
   fmt.Println(nextNumber1()) //1 重新计数了
   fmt.Println(nextNumber1()) //2
}
```

## 数组

数组声明

```
//声明
var balance [10] float32
//声明同时初始化，
var balance = [...]float32{1000.0, 2.0, 3.4, 7.0, 50.0}
//或 长度不固定用...代替
balance := [...]float32{1000.0, 2.0, 3.4, 7.0, 50.0}

//数组某位置的值赋值
var salary float32 = balance[9]
//内置方法求数组长度
len(balance)
```

数组的读取其实和c就一样了。

## 结构体

结构体的定义

```
//type 名称 struct
type Request struct {
	变量 类型
	Headers map[string]string `json:"headers"`
	Params  map[string]string `json:"params"`
}
//结构体的指针
var rptr *Request
rptr = &request //和c类似了
```

## 动态数组slice

```
var slice1 []type = make([]type, len)
也可以简写为
slice1 := make([]type, len)
//也可以用第三个参数指定容量
make([]T, length, capacity)

//对于slice使用range语法
for i, num := range nums {
  if num == 3 {
  	fmt.Println("index:", i)
  }
}
```

## map

```
//声明方式
var map_variable map[key_data_type]value_data_type
//make方式
map_variable := make(map[key_data_type]value_data_type)

//创建集合
var countryCapitalMap map[string]string /*创建集合 */
countryCapitalMap = make(map[string]string)


/*查看元素在集合中是否存在 */
capital, ok := countryCapitalMap [ "American" ] /*如果确定是真实的,则存在,否则不存在 */
/*fmt.Println(capital) */
/*fmt.Println(ok) */
if (ok) {
	fmt.Println("American 的首都是", capital)
} else {
	fmt.Println("American 的首都不存在")
}
```

## 语言接口

```
package main

import (
    "fmt"
)
//接口
type Phone interface {
    call()
}

type NokiaPhone struct {
}
//实现call方法
func (nokiaPhone NokiaPhone) call() {
    fmt.Println("I am Nokia, I can call you!")
}

type IPhone struct {
}
//实现call方法
func (iPhone IPhone) call() {
    fmt.Println("I am iPhone, I can call you!")
}

func main() {
    var phone Phone
		
		//传入具体对象进行调用
    phone = new(NokiaPhone)
    phone.call()
		//传入具体对象进行调用
    phone = new(IPhone)
    phone.call()

}
```



## 异常

```
package main

import (
    "fmt"
)

// 定义一个 DivideError 结构
type DivideError struct {
    dividee int
    divider int
}

// 实现 `error` 接口 按照语言接口讲的实现Error方法
func (de *DivideError) Error() string {
    strFormat := `
    Cannot proceed, the divider is zero.
    dividee: %d
    divider: 0
`
    return fmt.Sprintf(strFormat, de.dividee)
}

// 定义 `int` 类型除法运算的函数
func Divide(varDividee int, varDivider int) (result int, errorMsg string) {
    if varDivider == 0 {
            dData := DivideError{
                    dividee: varDividee,
                    divider: varDivider,
            }
            errorMsg = dData.Error()
            return
    } else {
            return varDividee / varDivider, ""
    }

}

func main() {
		// if可以分为两段逻辑，先执行前面的逻辑，然后进入判断逻辑
    // 正常情况
    if result, errorMsg := Divide(100, 10); errorMsg == "" {
            fmt.Println("100/10 = ", result)
    }
    // 当除数为零的时候会返回错误信息
    if _, errorMsg := Divide(100, 0); errorMsg != "" {
            fmt.Println("errorMsg is: ", errorMsg)
    }

}
```



# 进阶教程

go tour

https://go.dev/tour/flowcontrol/6



腾讯go教程

https://cloud.tencent.com/developer/doc/1101