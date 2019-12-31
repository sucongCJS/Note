```c++
int main()
{
    string str("Hello World!\n");
    string::size_type ss = str.size()

    return 0;
}		
```

 `size` 操作返回的是 `string::size_type` 类型的值 

 `unsigned` 型  可以保证足够大能够存储任意 `string` 对象的长度 

 有些机器上 `int` 变量的表示范围太小, 为了避免溢出，保存一个 `stirng` 对象 `size` 的最安全的方法就是使用标准库类型 `string::size_type`。 

# 分割数组

```c++
void split(const string& s, vector<string>& tokens, const string& delimeters=" "){ 
    // const是因为参数s可能是const的??
    // 参数是引用的目的是为了提高效率, 传递引用速度更快, 内存使用更少
    string::size_type beginPos = s.find_first_not_of(delimeters, 0);
    string::size_type endPos = s.find_first_of(delimeters, beginPos);
    while(beginPos != string::npos || endPos != string::npos){
        // string::npos是一个很大的数字, 表示找不到
        tokens.push_back(s.substr(beginPos, endPos-beginPos));
        beginPos = s.find_first_not_of(delimeters, endPos);
        endPos = s.find_first_of(delimeters, beginPos);
    }
}
```

sregex_token_iterator pos(data.cbegin(),data.cend(),reg,{0,2});//0代表了获取整个match，2代表获取第二个group;-1代表了想知道所有子序列。 

```c++
#include <sstream>

int main(){
    string s = "abc cde edf";
	istringstream ss(s);
    string word;
    whlie(ss>>word)
        cout<<word;
}

```

