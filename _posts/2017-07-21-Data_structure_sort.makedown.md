---
layout:   post
title:    "数据结构之排序"
subtitle: "若我愿意等，最后的，最后的，你会和我一起吗？"
date:     2017-07-21
author:   "NL"
header-img: "img/post-bg-2015.jpg"
tags:
    - data_structure
---

```c++
#include<iostream>
#include<cstdio>
#include<vector>
#include<algorithm>
using namespace std;
template<typename T>
class Sort{
	public:
		Sort();
		~Sort();
		void add(T x);           //添加元素
		int getsize()const;      //得到元素的size
		void bubblesort();       //冒泡排序
		bool bubble(int l, int r);
		void Swap(T &a, T &b);
		void Print();             //打印元素
		void mergesort(int l, int r);  //归并排序
		void merge(int l,int m,int r); //归并合并
	private:
		vector<T>vec;
};


template<typename T>
void Sort<T>::add(T x) {
	vec.push_back(x);
}

template<typename T>
int Sort<T>::getsize()const {
	return vec.size();
}	

template<typename T>
Sort<T>::Sort() {
	vec.clear();
}

template<typename T>
Sort<T>::~Sort() {
}

template<typename T>
void Sort<T>::Swap(T &a, T &b) {
	T t = a;
	a = b;
	b = t;
}

template<typename T>
bool Sort<T>::bubble(int l, int r) {
	bool flag = true;
 	while (++l < r) {
		if (vec[l-1] > vec[l])
			flag = false, Swap(vec[l-1], vec[l]);
	}
	return flag;
}

template<typename T>
void Sort<T>::bubblesort() {
	int r = vec.size();
	while (!bubble(0, r--));
}

template<typename T>
void Sort<T>::Print() {
	for (int i=0; i<vec.size(); i++)
		cout<<vec[i]<<' ';
	cout<<endl;
}

template<typename T>
void Sort<T>::mergesort(int l, int r) {
	if (r-l < 2)
		return ;
	int m = (l+r)>>1;
	mergesort(l, m);
	mergesort(m, r);
	merge(l, m, r);
}
template<typename T>
void Sort<T>::merge(int l, int m, int r) {
	int lb = m-l;
	int lv = l;
	T *B = new T[lb];
	for (int i=0; i<lb; B[i++] = vec[lv++]);          
	for (int i=l, j=0, k=m; (j < lb || k < r); ) {    //合并前后两部分
		if ((j < lb) && (!(k<r) || B[j] <= vec[k]))
			vec[i++] = B[j++];
		if ((k < r) && (!(j < lb) || vec[k] < B[j]))
			vec[i++] = vec[k++];
	}
	delete[] B;
}


int main() {
	int n, x;
	Sort<int>*p = new Sort<int>();
	cin>>n;
	for (int i=0; i<n; i++){
		cin>>x;
		p->add(x);
	}
	p->mergesort(0, p->getsize());
	p->Print();
	cout<<p->getsize()<<endl;
	return 0;
}
```

