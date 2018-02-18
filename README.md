# BFS_tu
广度优先遍历无向图
就是一层一层的遍历一个图
所以我们用到队列
找一个起始点
遍历所有与其相关的点入队
深度优先遍历无向图
就是一条道走到尽头再回去
#include "iostream"
#include <vector>
#define Inf 999999
using namespace std;
vector<vector<int>> e;
vector<int> k;
int n, m,Min = Inf;
int c1, c2;
void dfs(int cur,int dis) {
	if (cur == c2) {
		if (dis < Min) {
			Min = dis;
		}
		return;
	}
	for (int i = 1; i <= n; i++) {
		if (e[cur][i] != Inf && !k[i]) {
			k[i] = 1;
			dfs(i, dis+e[cur][i]);
			k[i] = 0;
		}
	}
}
int main() {
	cin >> n >> m;
	cin >> c1 >> c2;
	e.resize(n + 1);
	for (int i = 1; i < n + 1; i++) {
		e[i].resize(n + 1);
		fill(e[i].begin(), e[i].end(), Inf);
	}
	for (int i = 1; i <= n; ++i)  e[i][i] = 0;
	 
	k.resize(n + 1);
	fill(k.begin(), k.end(), 0);
	for (int i = 0; i < m; ++i) {
		int a, b, l;
		cin >> a >> b >> l;
		e[a][b] = l;
		e[b][a] = l;
	}
	k[c1] = 1;
	dfs(c1, 0);
	cout << Min << endl;
	system("pause");
}
