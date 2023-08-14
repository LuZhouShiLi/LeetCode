# 剑指 Offer 05. 替换空格

## 解题思路


### 使用StringBuilder

* 创建一个StringBuilder
* 将字符串转换为字符数组 遍历字符数组
* 遇到不是空格的字符添加到Builder  如果是空格 添加%20
* 将builder对象转换为String

```java
class Solution {
    public String replaceSpace(String s) {
        // 双指针 前后指针
        // 将字符串转化字符数组
        char[] ch = s.toCharArray();

        // 统计字符串中空格的个数
        int count = 0;
        for(char a:ch){
            if(a == ' '){
                count++;
            }
        }

        // 创建一个StringBuilder
        StringBuilder builder = new StringBuilder();
        String chs = "%20";

        for(char n:ch){
            if(n != ' '){
                builder.append(n);
            }else{
                builder.append(chs);
            }
        }

        return builder.toString();

    }
}

```


### 双指针

* 首先计算有多少个空格
* 然后创建一个新的字符数组 容量为原来的数组长度 + 空格数量 * 2
* 定义两个指针
* 一个指针指向原始字符串最后一个位置 另一个指针指向扩展字符串的最后一个位置
* 最后遍历字符数组，如果左指针指向的字符不是空格那么直接赋值 如果是空格 赋值20%


```java
class Solution {
    public String replaceSpace(String s) {
        if(s == null || s.length() == 0){
            return s;
        }
        // 双指针 前后指针
        // 将字符串转化字符数组
        char[] chars = s.toCharArray();

        // 创建一个StringBuilder
        StringBuilder builder = new StringBuilder();

        // 统计字符串中空格的个数
        int count = 0;
        for(char a:chars){
            if(a == ' '){
                count++;
                builder.append("  ");
            }
        }
        // 左指针 指向原始字符串的最后一个位置
        int left = s.length() - 1;
        s += builder.toString();

        // 右指针指向 扩展字符串的最后一个位置
        int right = s.length() - 1;
        chars = s.toCharArray();
        // 从后面向前面进行遍历
        while(left >= 0){
            if(chars[left] == ' '){
                chars[right--] = '0';
                chars[right--] = '2';
                chars[right] = '%';
            }else{
                chars[right] = chars[left];
            }
            left--;
            right--;
        }
        return new String(chars);
    }
}
```