### 使用数组实现一个顺序的串结构
## 为该串结构提供丰富的操作，比如插入子串、在指定位置移除给定长度的子串、在指定位置取子串、连接串、串匹配等。

**根据OCP开闭原则，首先定义一个抽象的接口，方便后续扩展新的串结构实现方式。**
+ 如下是定义的**SelfString**接口，包含的该串结构需要包含的必要操作
```java
public interface SelfString {

    String insertSubString(int begain,String s);

    String getSubString(int begain,int end);

    String concat(String s);

    String deleteSubString(int begain,int length);

    int index(String s);

    String toString();

}
```

+ 接下来是使用数组的方式去实现这个接口

```java
import java.util.Arrays;
import java.util.Set;

public class ArrayString implements SelfString {

    private  String[] string;

    public ArrayString(String s){

        if (s!=null){
            string = new String[s.length()];
            for(int i=0;i<s.length();i++){
                string[i] = s.substring(i,i+1);
            }
        }
    }

    public int length(){
        return string.length;
    }


    @Override
    public String insertSubString(int begain, String s) {

        StringBuilder  res = new StringBuilder();

        for (int i=0;i<=begain;i++){
            res.append(string[i]);
        }
        res.append(s);
        for (int i=begain+1;i<string.length;i++){
            res.append(string[i]);
        }

        return res.toString();
    }

    @Override
    public String getSubString(int begain, int end) {
        StringBuilder res = new StringBuilder();
        for (int i=begain;i<end;i++){
            res.append(string[i]);
        }
        return res.toString();
    }

    @Override
    public String concat(String s) {
        StringBuilder res = new StringBuilder();
        for (int i=0;i<string.length;i++){
            res.append(string[i]);
        }
        return res.append(s).toString();
    }

    @Override
    public String deleteSubString(int begain, int length) {
        StringBuilder res = new StringBuilder();
        for (int i=0;i<begain;i++){
            res.append(string[i]);
        }
        for (int i=begain+length-1;i<string.length;i++){
            res.append(string[i]);
        }
        return res.toString();
    }

    @Override
    public int index(String s) {
        int length = s.length();
        for (int i=0;i<string.length;i++){
            if (string[i].equals(String.valueOf(s.charAt(0)))){
                int count = 0;
                for (int j=0;j<s.length();j++){
                    if (string[j].equals(String.valueOf(s.charAt(0)))){
                        count++;
                    }
                }
                if (count==s.length())
                    return i;
            }

        }
        return -1;
    }

    @Override
    public String toString() {
        return "ArrayString{" +
                "string=" + Arrays.toString(string) +
                '}';
    }

    public static void main(String[] args) {

        ArrayString s = new ArrayString("abc");
        System.out.println(s.toString());
        System.out.println(s.insertSubString(1,"bcs"));
        System.out.println(s.getSubString(0,1));
        System.out.println(s.concat("12332"));
        System.out.println(s.deleteSubString(0,2));
        System.out.println(s.index("s"));


    }
}

```

**关于 index方法，我这边用的是最笨的逐一比较的方式，总感觉应该有时间复杂度更低的方式，后续会更新**
