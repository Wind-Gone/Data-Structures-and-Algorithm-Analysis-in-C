## **🌲 第二章  算法分析



> East China Normal University
>
> Author: Wind-Gone





##### 1.1 假设需要生成前N个整数的一个随机置换。例如，l4,3,1,s,2！和13,1,4,2,5}就是合法 的置换，但lS,4,1,2,1}则不是，因为数1出现两次而数3却没有。这个程序常常用于模拟一些算法。我们假设存在一个随机数生成器r,它有方法randin七(i,))，它以相同的概率生成立和j之间的整数。下面是三个算法：如下填人从a[O]到a[n-1]的数组a;为了填入a[i]，生成随机数直到它不同于已经生成的a[o],a[ 1]，…，a[i-1]时再将其填入a[i]。

###### Algorithm-1 :

```c++
#include<bits/stdc++.h>
using namespace std;

int RandInt(int i ,int j){
    static default_random_engine engine(time(0));
    static uniform_int_distribution<unsigned> display(i,j);
    return display(engine); 
}


int main(int argc, char const *argv[])
{
    int N;
    cin>>N;
    vector<int> A;
    while (A.size()<N)
    {
        int rand_num = RandInt(0,N);
        bool flag = true;
        for (size_t i = 0; i < A.size(); i++)
        {
            if(A[i] == rand_num)
                flag=false;
        }
        if (flag)
            A.push_back(rand_num);
    }
    for(auto var : A)
    {
        cout<<var<<" ";
    }    
    cout<<endl;
    return 0;
}

```



借鉴dalao代码进行格式上的改进：

```c++
#include<bits/stdc++.h>
using namespace std;

int RandInt(int i ,int j){
    static default_random_engine engine(time(0));
    static uniform_int_distribution<unsigned> display(i,j);
    return display(engine); 
}


int main(int argc, char const *argv[])
{
    int N;
    cin>>N;
    vector<int> A;
    while (A.size()<N)
    {
        int rand_num = RandInt(0,N);
        if(none_of(A.begin(),A.end(),[rand_num](int k){return k == rand_num;}))   //true only when none of elements is equal to the random number
			A.push_back(rand_num);
    }
    for(auto var : A)
    {
        cout<<var<<" ";
    }    
    cout<<endl;
    return 0;
}

```



###### Algorithm-2: 

```c++
#include<bits/stdc++.h>
using namespace std;

int RandInt(int i ,int j){
    static default_random_engine engine(time(0));
    static uniform_int_distribution<unsigned> display(i,j);
    return display(engine); 
}


int main(int argc, char const *argv[])
{
    int N;
    cin>>N;
    vector<int> A;
    vector<int> Used(N, 0);
    while (A.size()<N)
    {
        int rand_num = RandInt(0,N);
        if(!Used[rand_num]){
            A.push_back(rand_num);
            Used[rand_num] = 1;
        }
			
    }
    for(auto var : A)
    {
        cout<<var<<" ";
    }    
    cout<<endl;
    return 0;
}

```

##### Algorithm-3: 

```c++
#include<bits/stdc++.h>
using namespace std;

void Swap(int* m,int* n)
{
	int temp = *m;
	*m = *n;
	*n = temp;
}


int RandInt(int i ,int j){
    static default_random_engine engine(time(0));
    static uniform_int_distribution<unsigned> display(i,j);
    return display(engine); 
}


int main(int argc, char const *argv[])
{
    int N;
    cin>>N;
    vector<int> A;
	for(int i = 0;i < N;++i)
		A.push_back(i+1);
	for(int i = 1; i < N;++i)
		Swap(&A[i],&A[RandInt(0,i)]);
    for(auto var : A)
    {
        cout<<var<<" ";
    }    
    cout<<endl;
    return 0;
}

```



