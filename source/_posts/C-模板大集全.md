---
title: C++模板大集全
date: 2019-12-03 16:56:33
tags:
password: Cindy
---
# P3378 【模板】堆
```cpp
#include<bits/stdc++.h>
using namespace std;
priority_queue<int>q;
int main()
{
	int n,k,QAQ;
	cin>>n;
	while(n--)
	{
		scanf("%d",&k);
		if(k==1)cin>>QAQ,q.push(-QAQ);
		if(k==2)printf("%d\n",-q.top());
		if(k==3)q.pop();
	}
}
```
# P3385 【模板】负环
```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<queue>
using namespace std;
#define maxn 3010
int T;
int ver[maxn<<1],head[maxn],Next[maxn<<1],edge[maxn<<1],tot;
int n,m,x,y,z;
template<class T>
void read(T&x)
{
	T ans=0;
	short f=1;
	char ch=getchar();
	while(ch<'0'||ch>'9')
	{
		if(ch=='-')f=-1;
		ch=getchar();
	}
	while(ch>='0'&&ch<='9')
	{
		ans=(ans<<1)+(ans<<3)+(ch^48);
		ch=getchar();
	}
	x=ans*f;
}
inline void add(int x,int y,int z)
{
	ver[++tot]=y;edge[tot]=z;
	Next[tot]=head[x];head[x]=tot;
}
void init()
{
	memset(head,0,sizeof head);
	tot=1;
	read(n);
	read(m);
	while(m--)
	{
		read(x),read(y),read(z);
		add(x,y,z);
		if(z>=0)add(y,x,z);
	}
}
int in[maxn];
bool v[maxn];
int d[maxn];
bool SPFA()
{
	queue<int>q;
	memset(v,0,sizeof v);
	memset(in,0,sizeof in);
	memset(d,0x3f,sizeof d);
	d[1]=0;
	q.push(1);
	in[1]++;
	while(q.size())
	{
		int x=q.front();q.pop();
		v[x]=0;
		for(int i=head[x];i;i=Next[i])
		{
			int y=ver[i],z=edge[i];
			in[x]++;
			if(in[x]==n)return 1;
			if(d[y]>d[x]+z)
			{
				d[y]=d[x]+z;
				if(!v[y])
				{
					v[y]=1;
					q.push(y);
				}
			}
		}
	}
	return 0;
}
int main()
{
	read(T);
	while(T--)
	{
		init();
		if(n==1)puts("YE5");
		else if(SPFA())puts("YE5");
		else puts("N0");
	}
}
```
# P3865 【模板】ST表
```cpp
#include<bits/stdc++.h>
#define maxn 100010
using namespace std;
template<class T>inline void read(T&__x){T __ans=0;char __ch=getchar();short __f=1;while(__ch<'0'||__ch>'9'){if(__ch=='-')__f=-1;__ch=getchar();}while(__ch>='0'&&__ch<='9'){__ans=(__ans<<1)+(__ans<<3)+(__ch^48);__ch=getchar();}__x=__ans*__f;}
int n,m,f[maxn][30],t,x,y;
int query(int l,int r)
{
	int k=log(r-l+1)/log(2.0);
	return max(f[l][k],f[r-(1<<k)+1][k]);
}
int main()
{
	read(n),read(m);
	for(int i=1;i<=n;i++)read(f[i][0]);
	t=ceil((double)log(n)/log(2.0));
	for(int j=1;j<=t;j++)
	for(int i=1;i<=n-(1<<j)+1;i++)
	f[i][j]=max(f[i][j-1],f[i+(1<<(j-1))][j-1]);
	while(m--)
	{
		read(x),read(y);
		printf("%d\n",query(x,y));
	}
}
```
# P2197 【模板】nim游戏
```cpp
#include<bits/stdc++.h>
using namespace std;
int T;
int k,x,ans;
int main() 
{
	cin>>T;
	while(T--)
	{
		ans=0;
		cin>>k;
		for(int i=1;i<=k;i++)
		cin>>x,ans^=x;
		if(ans)cout<<"Yes"<<endl;
		else cout<<"No"<<endl;
	}
}
```
# P3367 【模板】并查集
```cpp
#include<bits/stdc++.h>
using namespace std;
int fa[10001],n,m,k,x,y;
int get(int x)
{              
	if(x==fa[x])return x;
	return fa[x]=get(fa[x]);
}
int main()
{              
	cin>>n>>m;
	for(int i=1;i<=n;i++)
	fa[i]=i;
	for(int i=1;i<=m;i++)
	{
		cin>>k>>x>>y;
		if(k==1)fa[get(x)]=get(y);
		else
		{
			if(get(x)==get(y))cout<<"Y"<<endl;
			else cout<<"N"<<endl;
		}
	}
}
```
# P3811 【模板】乘法逆元
```cpp
#include<bits/stdc++.h>
using namespace std;
long long n,p,inv[3000001];
int main()
{
	cin>>n>>p;
	inv[1]=1;
	for(int i=2;i<=n;i++)
    inv[i]=(p-p/i)*inv[p%i]%p;
    for(int i=1;i<=n;i++)
    printf("%lld\n",inv[i]);
}

```
# P1177 【模板】快速排序
```cpp
#include<bits/stdc++.h>
using namespace std;
int a[100001];
int main()
{
    int n;
    cin>>n;
    for(int i=0;i<n;i++)cin>>a[i];
    sort(a,a+n);
    for(int i=0;i<n;i++)
    cout<<a[i]<<' ';
}
```