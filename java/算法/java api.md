

# 结构转换

## List```<String> ```to String[] 

```
//List<String> ---> String[]
String[] s = list.toArray(new String[0]); //效率最好
```

## int[] to List```<Integer>```

```
int[] a = new int[10];
List<Integer> list = new ArrayList<>(Arrays.asList(a));
```


## Long to Integer

```
Long l ;
Integer i = l.intValue();
```