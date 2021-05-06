# 20DynamicProgrammingProblems

## 1) LCS 

```c++
int lcs(int x, int y, string s1, string s2)
    {
        int dp[x+1][y+1];
        for(int i=0 ; i<=x ; ++i)
        {
            for(int j=0 ; j<=y ; ++j)
            {
                if(i==0 || j==0)
                    dp[i][j]=0;
                else if(s1[i-1]==s2[j-1])
                    dp[i][j]=1+dp[i-1][j-1];
                else
                    dp[i][j]=max(dp[i-1][j],dp[i][j-1]);
            }
        }
        return dp[x][y];
    }
```

## 3) Edit Distance O(n*n)

```c++
int editDistance(string s, string t) {
            int sn=s.size();
            int tn=t.size();
            int dp[sn+1][tn+1];
            for(int i=0 ; i<=sn ; ++i)  
            {
                for(int j=0 ; j<=tn ; ++j)
                {
                    if(i==0)
                        dp[i][j]=j;
                    else if(j==0)
                        dp[i][j]=i;
                    else if(s[i-1]==t[j-1])
                        dp[i][j]=dp[i-1][j-1];
                    else
                        dp[i][j]=1+min(dp[i][j-1],min(dp[i-1][j],dp[i-1][j-1]));
                }
            }
            return dp[sn][tn];
    }

```
## ) Maximum path sum in matrix  O(n*n)

```c++
int maximumPath(int N, vector<vector<int>> Matrix)
    {  
        for(int i=N-1 ; i>=0 ; --i)
        {
            for(int j=0 ; j<N ; ++j)
            {
                int d=(i==N-1)?0:Matrix[i+1][j];
                int dl=(i==N-1 || j==0)?0:Matrix[i+1][j-1];
                int dr=(i==N-1 || j==N-1)?0:Matrix[i+1][j+1];
                Matrix[i][j]+=max(d,max(dl,dr));
            }
        }
        int ans=0;
        for(int i=0 ; i<N ; ++i)
            ans=max(ans,Matrix[0][i]);
        return ans;    
    }

```
## 7) Equal Partition Problem  O(n*(sum of elements))

```c++
int equalPartition(int n, int a[])
    {
       int sum=0;
       for(int i=0 ; i<n ; ++i)
        sum+=a[i];
       if(sum%2!=0)
        return 0;
        sum=sum/2;
        bool dp[n+1][sum+1];
        for(int i=0 ; i<=n ; ++i)
        {
            for(int j=0 ; j<=sum ; ++j)
            {
                if(i==0 && j==0)
                        dp[i][j]=true;
                else if(i==0)
                        dp[i][j]=false;
                else if(j==0)
                        dp[i][j]=true;
                else if(a[i-1]<=j)
                {
                    dp[i][j]=dp[i-1][j]||dp[i-1][j-a[i-1]];
                }
                else
                    dp[i][j]=dp[i-1][j];
            }
        }
        return dp[n][sum];
    }

```
## 8) Optimal Strategy For A Game (Recursive ) 

```c++
long long ansfor(int a[] , int i , int j)
{
    if(dp[i][j]!=-1)
        return dp[i][j];
    if(j<=i)
        return 0;
    else
        dp[i][j]= max(a[i]+ min(ansfor(a,i+2,j) ,ansfor(a,i+1,j-1) ),a[j]+min( ansfor(a,i,j-2) ,ansfor(a,i+1,j-1)) );

    return dp[i][j] ;
}

long long maximumAmount(int a[], int n) 
{
    memset(dp,-1,sizeof(dp));
    return ansfor(a,0,n-1);
}
```


