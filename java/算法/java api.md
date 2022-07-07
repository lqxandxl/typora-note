# 基本结构

byte 1字节

short 2字节

int 4字节

long 8字节

float 4字节

double 8字节

boolean 内存中至少1字节

浮点除以0变为NAN NAN不等于NAN

整数除以0报错

null



# 数学基本计算

java.lang.Math

向上取整用Math.ceil(double a)

向下取整用Math.floor(double a)

开平方 Math.sqrt()

Math.max

Math.min

java.lang.Long.MAX_VALUE

java.lang.Long.MIN_VALUE



# 数组

int[] 是一种引用

一维数组的初始化：

int[] a = new int[5];

二维数组的初始化：

```
int[][] a = new int[4][];

a[0] = new int[2];
```

java5之后的遍历方式：

for(String s: books){} //foreach方法

int[] res = new int[2]; //初始化

nums.length 求长度

Arrays.sort(nums); //数组的排序



# 字符串处理

String 是否可以修改单个内容？如何修改？

String str

str.charAt(i) //取值 得 Character

字符串分割？子串？连接？

str.substring(beginIndex,endIndex)

str.trim() 

String的修改和插入没有方便记忆的办法，采用和python一致的拼接方法。

String到数字的相互转化？ 只要记住valueOf就可以了。

Integer-->String

String str = String.valueOf(a);

String --> Integer

Integer i = Integer.valueOf(str);

求长度：

s.length



# 高级排序与lambda

```
int [][]a = new int [5][2];

Arrays.sort(a, new Comparator<int[]>() { //int[] 作为比较的类型
@Override
public int compare(int[] o1, int[] o2) {
  if (o1[0]==o2[0]) return o1[1]-o2[1];
  return o1[0]-o2[0];
  }
});


lambda则是
xxx -> {} 的形式

对于ArrayList则是
Collections.sort(list, comp);
public class Mycomparator implements Comparator {

    public int compare(Object o1, Object o2) {
        Person p1 = (Person) o1;//强转然后进行比较
        Person p2 = (Person) o2;
        if (p1.age < p2.age) return 1;
        else return 0;
    }

}
```



# List

```
//add
a.add(x)
a.add(index,x)
//get
a.get(index)
//delete
a.remove(index)
//edit
a.set(index,x)
//排序 
Collections.sort(list)
```

# Set

s = new HashSet

s.add(k)

s.remove(k)

//get

s.contains(k) //return boolean

//迭代 直接使用迭代器迭代 和Map里面的方法类似

set中存储元素先判断hashCode是否重复，如果重复再进行equals的比较，equals默认比较的是内存的地址。

如果set中存储Person对象，Person想要靠比如name属性来判断是否是一致的元素，这个时候就需要重新写equals的逻辑来比较对象。

默认的hashCode方法是把对象内存地址进行hash。因此为了让set可以使用name标准进行Person存储，需要重写hashCode。

```
       //重写equals()
        @Override
        public boolean equals(Object obj) {
            if (obj == null || !(obj instanceof Person)) {
                return false;
            }
            //地址相同必相等
            if (obj == this) {
                return true;
            }
            Person person = (Person) obj;
            //地址不同比较值是否相同
            return person.name.equals(this.name);
        }

        //重写hashCode()
        @Override
        public int hashCode() {
            return Objects.hash(name);
        }

        重写equals()必须重写hashCode() //原则！
```



# 字典

//add

m.put(k,v)

//del

m.remove(k)

m.remove(k,v)

//判断是否包含key

m.containsKey(key) //return boolean  //Map下的T必须是类而不是基本类型

//get

m.get(k) //return v //先判断有无

//foreach

```
for (k : m.keySet()){ //keySet返回set集合
}
```

//原理性 foreach
```
for(Map.Entry<k,v> e:m.entrySet()){
    e.getKey() //Entry方法
    e.getValue()
}
```

//迭代器
```
Iterator<T> it = 集合<T>.iterator()
while(it.hasNext())
    T = it.next()
//由此推之
Iterator<Map.Entry<k,v>> it = m.entrySet().iterator() //Entry作为内部类

```

T必须是类，不能是基本类型。

//省却大量语句，如果没获取到单词就赋值0+1，如果有获取到单词就是单词value再+1

dict.put(word,dict.getOrDefault(word,0)+1);