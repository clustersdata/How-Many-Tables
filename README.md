# How-Many-Tables

How Many Tables

Problem Description

Today is Ignatius' birthday. He invites a lot of friends. Now it's dinner time. Ignatius wants to know how many tables he needs at least. You have to notice that not all the friends know each other, and all the friends do not want to stay with strangers.


One important rule for this problem is that if I tell you A knows B, and B knows C, that means A, B, C know each other, so they can stay in one table.


For example: If I tell you A knows B, B knows C, and D knows E, so A, B, C can stay in one table, and D, E have to stay in the other one. So Ignatius needs 2 tables at least.

Input

The input starts with an integer T(1<=T<=25) which indicate the number of test cases. Then T test cases follow. Each test case starts with two integers N and M(1<=N,M<=1000). N indicates the number of friends, the friends are marked from 1 to N. Then M lines follow. Each line consists of two integers A and B(A!=B), that means friend A and friend B know each other. There will be a blank line between two cases.

Output

For each test case, just output how many tables Ignatius needs at least. Do NOT print any blanks.

Sample Input

2 5 3 1 2 2 3 4 5 5 1 2 5

Sample Output

2 4

代码：#include <stdio.h>

#define MAX 2000

int n,m;

int start[MAX],end[MAX];

int res;

int arr[MAX];

int len;

int Mempty()

{

    int i;
    
    for(i=0;i<m;i++)
    
        if(start[i]!=0) return 0;
        
    return 1;
}

int inSet(int index)

{
    int i;
    
    for(i=0;i<res;i++)
    
        if(arr[i]==index) return 1;
        
    return 0;
    
}

void deal()

{
    int i;
    
    int space=0;
    
    for(i=0;i<m;i++)
    
    {
        if(start[i]==0) space++;
        
        else  {  start[i-space]=start[i];  end[i-space]=end[i];   }
        
    }
    
    m=m-space;
    
    
}

void proc()

{
    int i;  int j;
    
    while(!Mempty())
    
    {
        i=0;
        
        while(i<m)
        
        {
            if(start[i]==0) {  i++;  continue;  }
            
            if(i==0)
            
            {
                if(start[i]!=end[i]) {  arr[res++]=start[i];  arr[res++]=end[i];   }
                
                else arr[res++]=start[i];
                
                start[i]=end[i]=0;
                
            }
            
            else
            
            {
            
                for(j=0;j<res;j++)
                
                {
                
                    if(arr[j]==start[i]) 
                    
                    {
                    
                        if(!inSet(end[i])) arr[res++]=end[i];
                        
                        start[i]=end[i]=0;
                        
                        i=-1;
                        
                        break;
                        
                    }
                    
                    if(arr[j]==end[i]) 
                    
                    {
                    
                        if(!inSet(start[i])) arr[res++]=start[i];
                        
                        start[i]=end[i]=0;
                        
                        i=-1;
                        
                        break;
                        
                    }
                    
                }
                
            }
            
            i++;
            
        }
        
        len++;  deal();
        
    }
    
    if(res==n) len--;
    
    else len+=n-res-1;
    
}

int main()

{

    int i;
    
    int num;
    
    scanf("%d",&num);
    
    while(num--)
    
    {
    
        scanf("%d%d",&n,&m);
        
        for(i=0;i<m;i++) scanf("%d %d",&start[i],&end[i]);
        
        res=0;  len=0;  proc();
        
        printf("%d\n",len+1);
        
    }
    
    return 0;
    
}
