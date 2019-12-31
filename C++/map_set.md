```c++
#include<string>  
#include<iostream>  
#include<unordered_map>
using namespace std;  
  
int main()
{
	unordered_map<string, int>  dict; // 声明unordered_map对象
	
	// 插入数据的三种方式
	dict.insert(pair<string,int>("apple",2));
	dict.insert(unordered_map<string, int>::value_type("orange",3));
	dict["banana"] = 6;
	
	// 判断是否有元素
	if(dict.empty())
		cout<<"1"<<endl;
	else
		cout<<"1"<<dict.size()<<"2"<<endl;
	
	// 遍历
	unordered_map<string, int>::iterator iter;
	for(iter=dict.begin();iter!=dict.end();iter++)
		cout<<iter->first<<ends<<iter->second<<endl;
	
	// 查找
	if(dict.count("boluo")==0)
		cout<<"can't find boluo!"<<endl;
	else
		cout<<"find boluo!"<<endl;
	
	if((iter=dict.find("banana"))!=dict.end())
		cout<<"banana="<<iter->second<<endl;
	else
		cout<<"can't find boluo!"<<endl;
	
	return 0;
}
```

