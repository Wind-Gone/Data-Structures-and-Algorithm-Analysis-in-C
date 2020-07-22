
## **🌲 第一章  引论

> East China Normal University
>
> Author: Wind-Gone



##### 1.1 编写一个程序解决选择问题。令k=N/2。画出表格显示程序对千N种不同的值的运行时间。

###### Algorithm-1 :

```c++
#include<bits/stdc++.h>
using namespace std;
int stored [100000];



void  BubbleSort(int* arr,int len){
    int tmp = 0;

    for (size_t i = 0; i < len-1; i++)
    {
        for (size_t j = 0; j <len-1-i ; j++)
        {
            if(arr[j]<arr[j+1])
			{
				tmp=arr[j];
				arr[j]=arr[j+1];
				arr[j+1]=tmp;
			}
        }
        
    }
    
}


int main(int argc, const char** argv) {
    memset(stored, 0 ,sizeof(int));
    //c++11中提出使用default_random_engine类和恰当的分布类对象来获取随机数
    static default_random_engine e(time(0));
    static uniform_int_distribution<unsigned> u(1,25000);//声明对象，设定随机数区间。
    ifstream in("ex1_1.1.txt"); //定义输入文件
    ofstream out("ex1_1.1.txt");
    double   duration;
    for(size_t i = 0; i <100000;i++){
        out<< u(e)<<" ";
    }
    int N = 0, input_num = 0;
    cin >> N;
    int k = N >>1;
    clock_t    start, end;
    start = clock();
    for (size_t i = 0; i < N; i++)
    {
        in>>input_num;
        // cout<<"input"<<" "<<input_num;
        stored[i] = input_num;
    }
    // cout<<endl;
    BubbleSort(stored,N);
    // for(auto item:stored)
    //     if(item!=0)
    //     cout<<item<<" ";
    // cout<<endl;
    cout<<stored[k-1]<<endl;
    end = clock();
    duration =  ((double)(end - start)) /  CLOCKS_PER_SEC;
	cout << "It took " << duration << " seconds" << endl;    //output the running time 
	return 0;
}
```





###### Algorithm-2: 

```c++
#include<bits/stdc++.h>
using namespace std;
int stored [100000];



void  BubbleSort(int* arr,int len){
    int tmp = 0;

    for (size_t i = 0; i < len-1; i++)
    {
        for (size_t j = 0; j <len-1-i ; j++)
        {
            if(arr[j]<arr[j+1])
			{
				tmp=arr[j];
				arr[j]=arr[j+1];
				arr[j+1]=tmp;
			}
        }
        
    }
    
}


int main(int argc, const char** argv) {
    memset(stored, 0 ,sizeof(int));
    //c++11中提出使用default_random_engine类和恰当的分布类对象来获取随机数
    static default_random_engine e(time(0));
    static uniform_int_distribution<unsigned> u(1,25000);//声明对象，设定随机数区间。
    ifstream in("ex1_1.1.txt"); //定义输入文件
    ofstream out("ex1_1.1.txt");
    double   duration;
    for(size_t i = 0; i <100000;i++){
        out<< u(e)<<" ";
    }
    int N = 0, input_num = 0;
    cin >> N;
    int k = N >>1;
    clock_t    start, end;
    start = clock();
    for (size_t i = 0; i < k; i++)
    {
        in>>input_num;
        // cout<<"input"<<" "<<input_num;
        stored[i] = input_num;
    }
    // cout<<endl;
    BubbleSort(stored,k);
    int surplus = N-k;
    while (surplus--)
    {
        in >> input_num;
        if (stored[k-1] >=input_num) continue;
        for (size_t i = k-2; i >=0; i--)
        {
            if(stored[i]>=input_num){
                for (size_t j = k-1; j != i+1 ; j--)
                {
                    stored[j] = stored[j-1];
                }
                stored[i+1] = input_num;
                break;
            }
        }
    }
    
    // for(auto item:stored)
    //     if(item!=0)
    //     cout<<item<<" ";
    // cout<<endl;
    cout<<stored[k-1]<<endl;
    end = clock();
    duration =  ((double)(end - start)) /  CLOCKS_PER_SEC;
	cout << "It took " << duration << " seconds" << endl;    //output the running time 
	return 0;
}
```



|             |  100  | 1000  | 10000 | 100000 |
| :---------: | :---: | :---: | :---: | :----: |
| Algorithm-1 | 0.001 | 0.008 | 0.199 | 23.854 |
| Algorithm-2 | 0.001 | 0.007 | 0.073 |  8.54  |



##### 1.2 编写一个程序求解字谜游戏问题。

```c++
#include<bits/stdc++.h>
using namespace std;
#include <vector>
int x_pos[8] = {0,0,1,1,1,-1,-1,-1};
int y_pos[8] = {1,-1,0,1,-1,0,1,-1};

vector <string> dict;
vector<vector<char>> word_list;

int main(int argc, char const *argv[])
{
    int input,dimension;
    string word ;
	char letter;
    cin>>input;
    while (input--)
    {
        cin>>word;
        dict.push_back(word);
    }
    cin>>dimension;
    word_list.resize(dimension);
    // for (int i = 0; i < dict.size(); i++)
    // {
    //     cout<<dict.at(i);
    // }
    
    for (size_t i = 0; i < dimension; i++)
    {
        for (size_t j  = 0; j < dimension; j++)
        {
            cin >> letter;
			word_list[i].push_back(letter);
        }
    }
    
    //(行，列，方向，字符数)
    for (size_t i = 0; i < dimension; i++)
    {
        for (size_t j = 0; j < dimension; j++)
        {
            for (size_t k = 0; k < 8; k++)
            {
                string str = "";
                int m =i;
                int n=j;
                for (size_t w = 0; w < dimension; w++)
                {
                    str+=word_list[m][n];
                    m +=x_pos[k];
                    n +=y_pos[k];
                    vector<string>::iterator it = find(dict.begin(), dict.end(), str);
                    if (it != dict.end())
                        cout<<str<<endl;
                    if (m < 0 || m >= dimension || n < 0 || n >= dimension)
                        break;  
                }
                
            }
            
        }
        
    }
        
    
    return 0;
}

```



##### 1.3 只使用处理1/0的printDigit方法，编写一种方法以输出任意double型量（可以是负的）。



##### 1.4 编写 一个程序，使它读入被一些 include 语句修饰的文件并且输出这个文件。
