```cpp
#include<iostream>
static const int maxNum = 25;
struct tuple//矩阵元素
{
	int i, j;//元素的行,列下标
	int value;//元素的值
};
struct spmatrix//稀疏矩阵
{
	int nx, ny, tu;//行数,列数,非零元素个数
	tuple data[maxNum];
};
//对两个以三元组形式存储的同阶稀疏矩阵A、B，设计算法求C = A + B。
spmatrix sum_spmatrix(const spmatrix& s1, const spmatrix& s2)
{
	spmatrix s3(s1);
	int a = s3.tu;
	for (int i = 0; i < s2.tu; i++)
	{
		bool s2_once = false;//判断s3中是否有与该s2元素为同行同列元素的元素
		for (int j = 0; j < a; j++)
		{
			if (s3.data[j].i == s2.data[i].i && s3.data[j].j == s2.data[i].j)
			{
				s3.data[j].value += s2.data[i].value;
				s2_once = true;
			}
		}
		if (!s2_once)
		{
			s3.data[s3.tu] = s2.data[i];
			s3.tu++;
		}
	}
	return s3;
}
int main()
{
	spmatrix s1, s2;
	s2.nx=s1.nx = 5, s2.ny=s1.ny = 5,s2.tu=s1.tu=0;
	for (int i = 0; i < 5; i++)
	{
		tuple t{i+1,i+1,i+10};
		s1.data[i] = t;
		s1.tu++;
	}
	for (int i = 0; i < 4; i++)
	{
		tuple t{ i + 1,i + 1,i + 1 };
		s2.data[i] = t;
		s2.tu++;
	}
	spmatrix s3;
	s3 = sum_spmatrix(s1, s2);
	std::cin.get();
	return 0;
}
```
