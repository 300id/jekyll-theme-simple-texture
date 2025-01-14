---
layout: post
title: "入门阶段"
description: "The first post"
categories: [ACM]
tags: [题解]

---

* Kramdown table of contents
{:toc .toc}

# Part 1 入门阶段
## Part 1.1 从零开始
### P1421 小玉买文具

基础语法，可以考虑扩大十倍用a*10+b / 19 来避免取整。
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;

    int main(){			

        int a, b;
        cin >> a >> b;
        cout << (a * 10 + b) / 19;
        system("pause");
        return 0;
    }
    {% endhighlight %}
</details>

### P1909 买铅笔
8说了，自己看吧
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;
    int n;
    int x, y, ans = INF;
    int main(){			

        cin >> n;
        for(int i = 1 ; i <= 3 ; ++ i){
            cin >> x >> y;
            ans = min(ans, ((n - 1) / x + 1) * y);
        }
        cout << ans;
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P1089 津津的储蓄计划
8说了，自己看吧
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;
    int a[13];
    int main(){			
        int ans = 0, mom = 0;
        for(int i = 1 ; i <= 12 ; ++ i){
            cin >> a[i];
            ans += 300;
            if(ans < a[i]){
                cout << "-" << i;
                // system("pause");
                return 0;
            }
            ans -= a[i];
            mom += ans / 100 * 100;
            ans %= 100;
        }
        cout << ans + mom * 1.2;
        system("pause");
        return 0;   
    }

    {% endhighlight %}
</details>

### P1085 不高兴的津津
8说了，自己看吧
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;
    int a, b, mx = -1, ans = 0;
    int main(){			
        for(int i = 1 ; i <= 7 ; ++ i){
            cin >> a >> b;
            if(a+b > 8 && a+b > mx){
                mx = a + b;
                ans = i;
            }
        }
        printf("%d", ans);
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P1035 级数求和
8说了，自己看吧
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;
    int main(){
        double ans = 0;
        int k;
        cin >> k;
        for(int i = 1 ; ; ++ i){
            ans += 1.0 / i;
            if(ans > k){
                cout << i << endl;
                break;
            }
        }
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P1980 计数问题
这题还是有点意思。
考虑最简单的思路，遍历然后计算每位的贡献，但是复杂度是nlog10(n)

但是还可以有log10(n)的写法
考虑计算每一位对所有答案的贡献。
比如1-10846为例，计算含目标数字不为0的情况，共有三种情况。

计算1-10846十位为7的个数：
此时a = 108 b=4 c=6 ，不难看出其实是将原数拆成了a，b，c三个部分
那么贡献=108 * 10 因为左边a从0~107与b=7再和c从0~9组合构成所有答案

计算1-10846十位为4的个数：
那么贡献=108 * 10 + 6 + 1 因为左边a从0~107与b=4再和c从0~9组合 + 左边a=108 b=4 c=0~6构成所有答案

计算1-10846十位为3的个数：
那么贡献=109 * 10 因为左边a从0~108与b=3再和c从0~9组合构成所有答案

**最后还要注意如果要计算的是0，情况还有所不同需要特殊判断。**
计算1-10846千位为0的个数
那么贡献=(1-1) * 1000 + 846 + 1 因为a从1~1 b=0 c从0~846组合构成所有答案

计算1-10846十位为0的个数
那么贡献=108 * 1000 因为a从1~108 b=0 c从0~9组合构成所有答案

<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;

    int main(){
        int n, x;
        cin >> n >> x;
        int t = 1, ans = 0;
        while(t <= n){
            int a = n / (t * 10);
            int b = n / t % 10;
            int c = n % t;
            if(x){
                if(b < x) ans += a * t;
                if(b == x) ans += a * t + c + 1;
                if(b > x) ans += (a + 1) * t;
            }
            else{
                if(b) ans += a * t;
                else ans += (a - 1) * t + c + 1;
            }
            t *= 10;
        }
        cout << ans << endl;
        system("pause");
        return 0;   
    }

    {% endhighlight %}
</details>

### P1014 Cantor表
不讨喜的规律题
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;
    ll n;
    int main(){
        cin >> n;
        ll i = 1;   
        while(i * (i + 1) / 2 < n) i ++;
        ll j = n - i * (i - 1) / 2;
        if(i&1) cout << i - j + 1 << '/' << 1 + j - 1;
        else cout << 1 + j - 1 << '/' << i - j + 1;
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P1307 数字反转
8说了，自己看
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;
    char s[15];
    int main(){
        scanf("%s", s + 1);
        int ln = strlen(s + 1);
        int i = 1, j = ln, ans = 0;
        if(s[i] == '-') i ++;
        while(j >= i) ans = ans * 10 + s[j] - '0', j --;
        if(i>1) cout << "-";
        cout << ans;
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

## Part 1.2 数组基础
### P1046 陶陶摘苹果
8说了，自己看吧
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;
    int x[11], ans;
    int main(){
        for(int i = 1 ; i <= 10 ; ++ i){
            cin >> x[i];
            x[i] -= 30;
        }
        cin >> x[0];
        for(int i = 1 ; i <= 10 ; ++ i){
            if(x[i] <= x[0]) ans ++;
        }
        cout << ans;
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P1047 校门外的树
暂时想到的三种解法

第一种，每个区间类似于染色标记，最后遍历一遍看哪些未被染色。复杂度O(m*l)

第二种，每个区间排序后合并，时间复杂度为O(mlogm)

第三种，写起来最方便，也是本题解的做法。考虑差分思想，每个起点+1，终点后面一个位置-1。最后遍历看0的数量。
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;
    int n, m, x, y, ans;
    int a[maxn];
    int main(){
        cin >> n >> m;
        for(int i = 1 ; i <= m ; ++ i){
            cin >> x >> y;
            a[x] += 1;
            a[y + 1] -= 1;
        }
        for(int i = 0 ; i <= n ; ++ i){
            if(i) a[i] = a[i-1] + a[i];
            if(a[i] == 0) ans ++;
        }
        
        cout << ans;
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P1427 小鱼的数字游戏
基础的栈思想
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;
    int x;
    stack<int> s;
    int main(){
        while(scanf("%d", &x) && x){
            s.push(x);
        }
        while(s.size()){
            printf("%d%c", s.top(), s.size()>1?' ':'\n');
            s.pop();
        }
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P2141 珠心算测验
注意读题，2+3=5和1+4=5只算一种
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 2e4 + 10;
    int n, x[102], len, vis[maxn], ans = 0;
    int main(){
        cin >> n;
        for(int i = 1 ; i <= n ; ++ i){
            cin >> x[i];
            vis[x[i]] ++;
        }
        sort(x + 1, x + 1 + n);
        len = unique(x + 1, x + 1 + n) - x - 1;
        for(int i = 3 ; i <= len ; ++ i){
            for(int j = 1 ; j < i ; ++ j){
                if(vis[x[i]-x[j]] && x[i]-x[j] < x[j]){
                    ans ++;
                    break;
                }
            }
        }
        cout << ans;
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P5594 【XR-4】模拟赛
8说了
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e3 + 10;
    int n, m, k;
    int a[maxn][maxn], x;
    int main(){
        cin >> n >> m >> k;
        for(int i = 1 ; i <= n ; ++ i){
            int p = 0;
            for(int j = 1 ; j <= m ; ++ j){
                cin >> x;
                a[x][++p] = 1;
            }
        }
        for(int i = 1 ; i <= k ; ++ i){
            int t = 0;
            for(int j = 1 ; j <= m ; ++ j) t += a[i][j];

            printf("%d%c", t, i!=k?' ':'\n');
        }
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

## Part 1.3 字符串基础
### P5015 标题统计
8说了
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e3 + 10;
    string s;
    int main(){
        getline(cin, s);
        int ans = 0;
        for(int i = 0 ; i < s.length() ; ++ i){
            if((s[i] <= 'z' && s[i] >= 'a') || (s[i] >= '0' && s[i] <= '9') || (s[i] >= 'A' && s[i] <= 'Z')){
                ans ++;
            }
        }
        cout << ans;
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P1055 ISBN号码
8说了
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e3 + 10;
    string s;
    int main(){
        cin >> s;
        int ln = s.length();
        int x = (s[0]-'0')*1 + (s[2]-'0')*2 + (s[3]-'0')*3 + (s[4]-'0')*4 + (s[6]-'0')*5 
        + (s[7]-'0')*6 + (s[8]-'0')*7 + (s[9]-'0')*8 + (s[10]-'0')*9;
        x %= 11;
        if(x == 10){
            if(s[12] == 'X') cout << "Right";
            else{
                cout << s.substr(0, 12) << 'X';
            }
        }
        else{
            if(s[12] == x + '0') cout << "Right";
            else{
                cout << s.substr(0, 12) << x;
            }
        }
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P1308 统计单词数
8说了
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e3 + 10;
    string s, t;
    int pos = -1, cnt;
    int main(){
        cin >> s;
        getchar();
        getline(cin, t);
        int ls = s.length();
        for(int i = 0 ; i < ls ; ++ i) if(s[i] <= 'Z' && s[i] >= 'A') s[i] = s[i] - 'A' + 'a';
        int lt = t.length();
        for(int i = 0 ; i < lt ; ++ i) if(t[i] <= 'Z' && t[i] >= 'A') t[i] = t[i] - 'A' + 'a';
        for(int i = 0 ; i < lt - ls ; ++ i){
            // cout << s[i] << ' ' << t[i] << ' ' << t .substr(i, ls) << endl;
            if(i == 0 || t[i-1] == ' '){
                if(s[0] == t[i] && t.substr(i, ls) == s && (t[i + ls] == ' ' || i + ls == lt - 1)){
                    cnt ++;
                    if(pos == -1) pos = i;
                    i = i + ls - 1;
                } 
            }
        }
        if(pos != -1) cout << cnt << ' ' << pos;
        else cout << pos;
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P2010 回文日期
只要枚举年份即可，反转前四位构成回文串再判断日期是否合法。
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 2e5 + 10;
    char s[maxn], t[maxn];
    int ans;
    int main(){ 
        scanf("%s", s); getchar();
        scanf("%s", t);
        int y1 = (s[0]-'0')*1000 + (s[1]-'0')*100 + (s[2]-'0')*10 + (s[3]-'0');
        int y2 = (t[0]-'0')*1000 + (t[1]-'0')*100 + (t[2]-'0')*10 + (t[3]-'0');
        int m1 = (s[4]-'0')*10 + s[5]-'0';
        int m2 = (t[4]-'0')*10 + t[5]-'0';
        int d1 = (s[6]-'0')*10 + s[7]-'0';
        int d2 = (t[6]-'0')*10 + t[7]-'0';
        for(int i = y1 ; i <= y2 ; ++ i){
            string p = to_string(i);
            int j = (p[3]-'0')*10+p[2]-'0';
            int k = (p[1]-'0')*10+p[0]-'0';
            if(j < 1 || j > 12 || k < 1 || k > 31) continue;
            if(j == 4 || j == 6 || j == 9 || j == 11){
                if(k >= 31) continue;
            }
            if(j == 2){
                if(i % 400 == 0 || (i % 4 == 0 && i % 100 != 0)){
                    if(k > 29) continue;
                }
                else{
                    if(k >= 29) continue;
                }
            }
            if(i == y1 && (j < m1 || (j == m1 && k < d1))) continue;
            if(i == y2 && (j > m2 || (j == m2 && k > d2))) continue;
            ans ++;
        }
        cout << ans;
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P1012 拼数
自定义排序。
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 2e5 + 10;
    int n;
    string s[30];
    int cmp(string a, string b){
        return a + b > b + a;
    }
    int main(){ 
        cin >> n;
        for(int i = 1 ; i <= n ; ++ i) cin >> s[i];
        sort(s + 1, s + 1 + n, cmp);
        for(int i = 1 ; i <= n ; ++ i) cout << s[i];
        system("pause");
        return 0;   
    }

    {% endhighlight %}
</details>

### P5587 打字练习
坑的一批，范文也有退格
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 2e5 + 10;
    string a[maxn], b[maxn];
    string get_str(string p){
        string x = "";
        for(int j = 0 ; j < p.length() ; ++ j){
            if(p[j] == '<'){
                if(!x.empty()){
                    x.pop_back();
                }
                continue;
            } 
            x = x + p[j];
        } 
        return x;
    }
    int main(){ 
        int la = 0, lb = 0;
        while(1){
            ++ la;
            getline(cin, a[la]);
            if(a[la] == "EOF"){
                la --; break;
            }
        }
        while(1){
            ++ lb;
            getline(cin, b[lb]);
            if(b[lb] == "EOF"){
                lb --; break;
            }
        }
        int t;
        cin >> t;
        int ans = 0;
        for(int i = 1 ; i <= min(la, lb) ; ++ i){
            string x = get_str(a[i]);
            string y = get_str(b[i]);
            
            for(int j = 0 ; j < min(x.length(), y.length()) ; ++ j){
                if(x[j] == y[j]) ans ++;
            }
            // cout << a[i] << "         " << x << endl;
        }
        printf("%d", (int)(ans * 1.0 * 60 / t + 0.5));
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

## Part 1.4 函数，递归及递推
### P1028 数的计算
记搜
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 2e5 + 10;
    int ans;
    int record[maxn];
    int dfs(int n){
        // cout << n << endl;
        if(record[n]){
            return record[n];
        }
        for(int i = n / 2 ; i >= 1 ; -- i){
            record[n] += dfs(i);
        }
        record[n] ++;
        return record[n];
    }
    int main(){ 
        int n;
        cin >> n;
        record[1] = 1;
        cout << dfs(n);
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P1036 选数
写麻烦了，本来想降一下复杂度的。
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 2e5 + 10;
    ll sum;
    int n, k, prime, ans;
    int vis[30];
    ll a[maxn];
    void dfs(int num, int f, ll he, int s){
        if(num == (f == 0 ? 20 - k : k)){
            if(f){
                prime = 1;
                for(int i = 2 ; i * i <= he ; ++ i){
                    if(he % i == 0){
                        prime = 0;
                        break;
                    }
                }
                if(prime) ans ++;
            }
            else{
                prime = 1;
                for(int i = 2 ; i * i <= he ; ++ i){
                    if((sum - he) % i == 0){
                        prime = 0;
                        break;
                    }
                }
                if(prime) ans ++;
            }
        }
        for(int i = s ; i <= n ; ++ i){
            if(!vis[i]){
                vis[i] = 1;
                dfs(num+1, f, he+a[i], i+1);
                vis[i] = 0;
            }
        }
    }
    int main(){ 
        cin >> n >> k;
        for(int i = 1 ; i <= n ; ++ i){
            cin >> a[i];
            sum += a[i];
        }
        
        if(k > 10) dfs(0, 0, 0, 1);
        else dfs(0, 1, 0, 1);
        cout << ans;
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P1464 Function
记忆化搜索
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;
    ll a, b, c;
    ll dp[21][21][21];
    ll w(ll a, ll b, ll c){
        if(a <= 0 || b <= 0 || c <= 0) return 1;
        if(a > 20 || b > 20 || c > 20) return w(20, 20, 20);
        if(dp[a][b][c]) return dp[a][b][c];
        if(a < b && b < c) return dp[a][b][c] = w(a, b, c-1) + w(a, b-1, c-1) - w(a, b-1, c);
        else return dp[a][b][c] = w(a-1, b, c) + w(a-1, b-1, c) + w(a-1, b, c-1) - w(a-1, b-1, c-1);
    }

    int main(){ 
        while(scanf("%lld %lld %lld", &a, &b, &c)){
            if(a==-1&&b==-1&&c==-1) break;
            printf("w(%lld, %lld, %lld) = %lld\n", a, b, c, w(a, b, c));
        }
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P5534 【XR-3】等差数列
公式
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;
    ll a, b, n;
    int main(){ 
        cin >> a >> b >> n;
        cout << (a + a + (n-1)*(b-a)) * n / 2 << endl;
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P1192 台阶问题
类似于斐波那契
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;
    int n, k;
    int dp[maxn];
    int main(){ 
        cin >> n >> k;
        dp[0] = 1;
        for(int i = 1 ; i <= n ; ++ i){
            for(int j = max(0, i-k) ; j < i ; ++ j){
                dp[i] = (dp[j] + dp[i]) % 100003;
            }
        }
        cout << dp[n];
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P1025 数的划分
dfs直接爆搜 or dp做

这题dp做还是很有意思的。数据增强版在这[U101024 数的划分(数据加强版)](https://www.luogu.com.cn/problem/U101024)

<details> 
    <summary>dfs爆搜解法</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 1e5 + 10;
    int n, k, ans;
    void dfs(int pos, int last, int sum){
        if(pos == k - 1){
            if(n - sum >= last) dfs(pos + 1, n - sum, n);
            return;
        }
        if(sum == n && pos == k){
            ans ++;
            return;
        }
        for(int i = last ; i + sum <= n ; ++ i){
            dfs(pos + 1, i, sum + i);
        }
    }
    int main(){ 
        cin >> n >> k;
        dfs(0, 1, 0);    
        cout << ans; 
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

我们考虑dp解法。那么原题目分数字其实可以转换为$n$个球要放进$k$个盒子，但是不能有空盒的方案数。

那么我们考虑$dp[i][j]$代表把$i$个球放入$j$个盒子，且不空盒的方案数

那么要不空盒，朴素的思想就是先取$j$个球在每个盒子中都放入一个，然后再把剩下的$i-j$个球放入$j$个盒子

那么显然有：

$$dp[i][j] = \sum_{k=1}^j dp[i-j][k]$$

这样子需要分别枚举$i，j，k$，时间复杂度为$O(nk^2)$
注意在枚举的时候要保证$i>=j$，不然没法分。
代码如下

<details> 
    <summary>O(n*k*k)解法dp</summary>
    {% highlight cpp %}
    cin >> n >> m;
    for(int i = 0 ; i <= n ; ++ i) dp[i][1] = 1;
    for(int i = 2 ; i <= n ; ++ i){
        for(int j = 2 ; j <= m ; ++ j){
            for(int k = 1 ; k <= j ; ++ k){
                if(i >= j)
                dp[i][j] += dp[i-j][k];
            }
        }
    }   
    cout << dp[n][m];
    {% endhighlight %}
</details>

但是其实还可以进一步优化到时间复杂度为$O(nk)$
对于上述转移方程我们考虑：

$$dp[i-1][j-1] = \sum_{k=1}^{j-1} dp[i-j][k]$$

等式右半之所以还是$i-j$是因为$(i-1) - (j-1) = i-j$

不难发现$dp[i][j]$和$dp[i-1][j-1]$只差了一项$dp[i-j][j]$

那么转移方程可以改写为：

$$dp[i][j] = dp[i-1][j-1] + dp[i-j][j]$$

此时只需要两层循环即可。
<details> 
    <summary>O(n*k)解法dp</summary>
    {% highlight cpp %}
    for(int i = 0 ; i <= n ; ++ i) dp[i][1] = 1;
    for(int i = 2 ; i <= n ; ++ i){
        for(int j = 2 ; j <= m ; ++ j){
            if(i >= j) dp[i][j] = dp[i-j][j] + dp[i-1][j-1];
        }
    }   
    cout << dp[n][m];
    {% endhighlight %}
</details>

但是对于强化版本的[U101024 数的划分(数据加强版)](https://www.luogu.com.cn/problem/U101024)我们还需要进一步优化空间复杂度才行。

其实因为k最大=600，所以每次更新dp数组只需要前面600个状态即可，这里考虑滚动数组来优化空间。
<details> 
    <summary>O(n*k)时间，O(k*k)空间解法dp</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 2e5 + 10;
    int n, m;
    short dp[601][601];
    int pos(int x){
        return (x % 600) + 1;
    }
    int main(){ 
        cin >> n >> m;
        dp[pos(0)][0] = 1;
        for(int i = 1 ; i <= n ; ++ i){
            memset(dp[pos(i)], 0, sizeof(dp[pos(i)]));
            for(int j = 1 ; j <= m && j <= i ; ++ j){
                dp[pos(i)][j] = (dp[pos(i-j)][j] + dp[pos(i-1)][j-1])%10086;
            }
        }   
        cout << dp[pos(n)][m];
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

### P4994 终于结束的起点
因为斐波那契循环节$<=6n$,所以暴力即可。
<details> 
    <summary>展开代码</summary>
    {% highlight cpp %}
    #include <bits/stdc++.h>
    #define endl '\n'
    #define ll long long
    #define PB push_back
    #define POP pop_back
    #define INF 0x3f3f3f3f
    using namespace std;
    const int maxn = 2e5 + 10;
    int n;
    int a[3];
    int main(){ 
        cin >> n;
        a[0] = 1; a[1] = 1;
        for(int i = 2 ; ; ++ i){
            if(a[0] == 0 && a[1] == 1){
                cout << i - 1;
                break;
            }
            a[2] = (a[0] + a[1]) % n;
            a[0] = a[1];
            a[1] = a[2];
        } 
        system("pause");
        return 0;   
    }
    {% endhighlight %}
</details>

[^1]: This is a footnote.

[kramdown]: https://kramdown.gettalong.org/
[Simple Texture]: https://github.com/yizeng/jekyll-theme-simple-texture

<!-- Link Gitalk 的支持文件  -->
<link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">
<script src="https://unpkg.com/gitalk@latest/dist/gitalk.min.js"></script>
<div id="gitalk-container"></div>
<script type="text/javascript">
    var gitalk = new Gitalk({

    // gitalk的主要参数
        clientID: '33599ca507921d70615d',
        clientSecret: '1e6229b3a409aac51d5d51dc5458a9c257ca59a9',
        repo: '300id.github.io',
        owner: '300id',
        admin: ['300id'],
        id:'2023-08-20-part1-scratch',

    });
    gitalk.render('gitalk-container');
</script>
<!-- Gitalk end -->

<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
<span id="busuanzi_container_site_uv"><br>
  本站总访客数<span id="busuanzi_value_site_uv"></span>人次
</span>
