---

title: MyTemp

date: 2019-12-10 17:13:29

tags:

---

```
#include<iostream>
#include<cstdio>
#include<algorithm>
#include<set>
using namespace std;
template<class T>
void read(T &x)
{
	T ans=0;short f=1;
	char ch=getchar();
	while(ch<'0'||ch>'9')
	{
		if(ch=='-')f=-1;
		ch=getchar();
	}while(ch>='0'&&ch<='9')
	{
		ans=(ans<<1)+(ans<<3)+(ch^48);
		ch=getchar();
	}x=ans*f;
}
#define maxn 200005
struct
{
	int l,r;
	set<int>s;
}tree[maxn<<2];
int n,m;
int l,r,k;
int a[maxn],p[maxn],t;
set<int>S[maxn];
void build(int x,int l,int r)
{
	int mid=(l+r)>>1;
	tree[x].l=l,tree[x].r=r;
	if(l==r)
	{
		tree[x].s=S[mid];
		return;
	}
	build(x<<1,l,mid);
	build(x<<1|1,mid+1,r);
	tree[x].s=tree[x<<1].s;
	for(set<int>::iterator it=tree[x<<1|1].s.begin();it!=tree[x<<1|1].s.end();it++)
	tree[x].s.insert(*it);
}
int ask(int x,int l,int r,int k)
{
	if(tree[x].l==tree[x].r)return l;
	int mid=(tree[x].l+tree[x].r)>>1;
	int val;
	val=*tree[x].s.lower_bound(tree[x].l)-*tree[x].s.lower_bound(tree[x].r-1);
	if(l<=mid)
	{
		if(val<k)return ask(x<<1,l,r,k);
		if(val>=k)return ask(x<<1,l,r,k-val);
	}
	if(r>mid)
	{
		if(val<k)return ask(x<<1|1,l,r,k);
		if(val>=k)return ask(x<<1|1,l,r,k-val);
	}
}
int main()
{
	read(n),read(m);
	for(int i=1;i<=n;i++)
		read(a[i]),p[i]=a[i];
	sort(p+1,p+n+1);
	t=unique(p+1,p+n+1)-p-1;
	for(int i=1;i<=n;i++)
	{
		a[i]=lower_bound(p+1,p+t+1,a[i])-p;
		S[a[i]].insert(i);
	}
	build(1,1,t);
	while(m--)
	{
		read(l),read(r),read(k);
		printf("%d\n",p[ask(1,l,r,k)]);
	}
}
```
![](/upload_file/【模板】可持久化线段树 1（树套树）.cpp)