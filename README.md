/*
自然语言描述：
贪心：越高位的数越大越好 
预处理从第i个位置开始，数字j出现的下一个位置 
对于第i位假设当前在pos，则看pos之后每个数字最先出现的位置k，检查k之后这个是否能填满还没填的数位
对于所有合法的位置k，选数字大的跳 
*/
#include<bits/stdc++.h>
using namespace std;
const int maxn=3e5+5;
int n,m,T;
int nxt[maxn][10];//从第i个位置开始，数字j出现的下一个位置 
char s[maxn];
int main(){
	cin>>s+1>>m;
	n=strlen(s+1);m=n-m;
	if(m<=0){
		cout<<"输入错误\n";
		return 0;
	}
	fill(nxt[n+1],nxt[n+1]+10,n+1);
	for(int i=n;i>=1;i--){
		memcpy(nxt[i],nxt[i+1],sizeof(nxt[i]));
		nxt[i][s[i]-'0']=i;
	}
	string res="";
	for(int i=9;i>=1;i--){
		int pos=nxt[1][i];
		if(n-pos+1<m)continue;//如果保留pos这个位置，后面要保证有足够的数字
		res+=s[pos];
		for(int j=1;j<m;j++){
			for(int k=9;k>=0;k--){
				if(nxt[pos+1][k]>n||n-nxt[pos+1][k]+1+j<m)continue;
				pos=nxt[pos+1][k];//跳到该位置 
				res+=s[pos];
				break;
			}
		}
		break;
	} 
	cout<<res<<"\n";
//	cin>>n>>m;
	
	return 0;
}
/*
100 2
*/


