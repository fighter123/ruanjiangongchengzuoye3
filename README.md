# ruanjiangongchengzuoye3
Main。Cpp
//四则运算
//李营；20142930；2016/3/21
#include "Arithmetic.h"

int main()
{
    P:
    Arithmetic A;//声明对象
    int N;//存储打印的题目数量
    int M;//存储参与混合运算的数字个数
    int n,m,f,o,p;
    cout<<"><><><><><><><><><><><><><><><"<<endl;
    cout<<"><      请选择模式：        ><"<<endl;
    cout<<"><       1为整数;           ><"<<endl;
    cout<<"><      2为假分数;          ><"<<endl;
    cout<<"><     3有括号运算          ><"<<endl;
    cout<<"><   4混合运算答题模式      ><"<<endl;
    cout<<"><><><><><><><><><><><><><><><"<<endl;
    cin>>n;
    cout<<"生成f值以内的运算题目（输入f值）："<<endl;
    cin>>f;
    if(n==1||n==2)
    {
        cout<<"请输入要打印的题目数量："<<endl;
        cin>>N;
        cout<<"有无乘除运算？（1没有，2有）："<<endl;
        cin>>m;
        cout<<"加减运算有无负数？(1没有，2有)："<<endl;
        cin>>o;
        cout<<"除法有无余数？（1没有，2有）"<<endl;
        cin>>p;
    }
    if(n==4)
    {
        cout<<"请输入参与混合运算的数字个数："<<endl;
        cin>>M;
    }
    switch(n)
    {
        case 1:
            {A.Intnumber(N,m,f,o,p);break;}
        case 2:
            {A.Mixnumber(N,m,f,o);break;}
        case 3:
            {A.Havespace(f,N);}
        case 4:
            {A.CeShi(M,f);}
        default:
            {
                cout<<"请按要求输入啦，亲！"<<endl;
                goto P;
            }
     }
     goto P;
     return 0;
}
.h文件
#pragma once
#include<iostream>
using namespace std;

class Arithmetic
{
protected:
    int a,b,c,d,y,m;
public:
    Arithmetic(void);
    ~Arithmetic(void);
    int Intnumber(int N,int m,int F,int O,int P);//整数函数
    int Mixnumber(int N,int m,int F,int O);//分数算式函数
    int show1(int y,int a,int b,int o,int P);//显示函数1
    int show2(int y,int a,int b,int c,int d);//显示函数2
    int Havespace(int F,int N);//有括号运算函数
    int CeShi(int N,int f);//产生测试题目函数
    char Operator();//产生运算符
    int PanDuan(float dd,int N,int number[1000],char oper[1000]);//d:传递用户输入的答案；N：传递用户所选混合运算的整数个数
};

Arithmetic.cpp文件
#include "Arithmetic.h"


Arithmetic::Arithmetic(void)
{
}


Arithmetic::~Arithmetic(void)
{
}
int Arithmetic::Intnumber(int N,int m,int F,int O,int P)
{
    for(int i=0;i<N;i++)
    {
           a=rand()%F;
           b=rand()%F;
           if(m==1)
           { y=rand()%2;}
           else if(m==2)
           { y=rand()%4;} //判断是否有乘除
           if(b==0||(a==b&&b==c)) //避免重复且除数不为0
             {
                i--;
             }        
            else
             {
                show1(y,a,b,O,P);
             }
           if((i+5)%4==0)
           {
                cout<<endl;
           }
    }
    return 0;
}
int Arithmetic::Mixnumber(int N,int m,int F,int O)
{
    for(int i=0;i<N;i++)
    {
         a=rand()%F;
         b=rand()%F;
         if(m==1)
           { y=rand()%2;}
         else if(m==2)
           { y=rand()%4;} //判断是否有乘除
         c=rand()%100;
         d=rand()%100; 
            if(b==0||b>=a||d>=c||(a==b&&b==c)) //确保假分数避免重复且除数不为0
            {
                i--;
            } 
            else
            {
                show2(y,a,b,c,d);
            }
        }
   return 0;
}
int Arithmetic::show1(int y,int a,int b,int o,int p)
{
      if(y==0)
        { 
           if(o==1)//判断有无负数
             {cout<<a<<"+"<<b<<"=   ";}
           else
              {
                if(rand()%3==0)//随机确定负号位置
                  {cout<<"(-"<<a<<")+"<<b<<"=   ";}
                if(rand()%3==1)
                  {cout<<a<<"+(-"<<b<<")=   ";}
                else
                  {cout<<"(-"<<a<<")+(-"<<b<<")=   ";}
              }
        }
      else if(y==1)//判断有无负数
        { 
            if(o==1)//随机确定负号位置
              {cout<<a<<"-"<<b<<"=   ";}
            else
              {
                if(rand()%3==0)
                  {cout<<"(-"<<a<<")-"<<b<<"=   ";}
                if(rand()%3==1)
                  {cout<<a<<"-(-"<<b<<")=   ";}
                else
                  {cout<<"(-"<<a<<")-(-"<<b<<")=   ";}
              }
        }
      else if(y==2)
        { cout<<a<<"*"<<b<<"=   ";}
      else
        if(p==1)//判断是否要求有余数
        {
            if(a%b!=0)
            {a=(a-a%b);}//确保没有余数
            cout<<a<<"/"<<b<<"=   ";
        }
        else
        {
            if(b==1)
            {b=b+1;}
            if(a%b==0)
            {a=(a+rand()%b);}//确保有余数
            cout<<a<<"/"<<b<<"=   ";
        }
    return 0;
}
int Arithmetic::show2(int y,int a,int b,int c,int d)
{
    if(y==0)
      {cout<<"("<<a<<"/"<<b<<")+("<<c<<"/"<<d<<")="<<endl;}
    else if(y==1)
      { cout<<"("<<a<<"/"<<b<<")-("<<c<<"/"<<d<<")="<<endl;}
    else if(y==2)
      {  cout<<"("<<a<<"/"<<b<<")*("<<c<<"/"<<d<<")="<<endl; }
     else
      {cout<<"("<<a<<"/"<<b<<")/("<<c<<"/"<<d<<")="<<endl; }
    
    return 0;
}
int Arithmetic::Havespace(int F,int N)
{
    
    for(int i=0;i<N;i++)
    {
        char s;
        int n=rand()%4;
        if(n==0)
        {s='+';}
        else if(n==1)
        {s='-';}
        else if(n==2)
        {s='*';}
        else
        {s='/';}
    cout<<"("<<rand()%F<<s<<rand()%F<<")"<<s<<"("<<rand()%F<<s<<rand()%F<<")="<<endl;
    }
    return 0;
}
char Arithmetic::Operator()//随机产生运算符
{
    char c;//存储运算符
    int r;
    r=rand()%4;
    if(r==0)
    {
        c='+';
    }
    else if(r==1)
    {
        c='-';
    }
    else if(r==2)
    {
        c='*';
    }
    else 
    {
        c='/';
    }
    return c;
}
int Arithmetic::CeShi(int N,int f)//实现混合运算式的输出
{
    int n=0;//用来计算作对数目
    for(int i=0;i<30;i++)//循环生成30道题目
    {
        int N1=N-1;//运算符个数
        char oper[1000];//用来存储运算符
        int number[1000];//用来存储参与运算的随机数
        for(int i=0;i<N;i++)//对参与运算的数依次赋值
        {
            number[i]=(rand()%f);
            if(number[i]==0)
            {
                i--;
            }
        }
         for(int i=0;i<N-1;i++)//对参与运算的运算符依次赋值
        {
            oper[i]=Operator();
        }
        oper[N-1]='=';
        for(int i=0;i<N;i++)//输出每一个混合运算式
        {
            int m;
            if(((oper[i]=='/')&&(oper[i-1]!='/'))||((oper[i]=='/')&&(oper[i-1]=='/')&&(oper[i-2]=='/')))
            //解决连续除号的如何加括号
            {
                cout<<"(";
                m=i;        
            }
            cout<<number[i];
            if(i==(m+1)&&oper[m]=='/')//后括号的输出
            {
                cout<<")";
            }
            cout<<oper[i];
        }
        cout<<"?";
        float D;//用来存储用户输入的答案
        cin>>D; 
        n=n+PanDuan(D,N,number,oper);
    }
    cout<<"您答对了"<<n<<"道题目"<<endl;
    return 0;
}
int Arithmetic::PanDuan(float dd,int N,int number[1000],char oper[1000])//判断混合运算用户单是否正确
{
        int n=0;//用来返回用户答案是否正确如正确返回1，错误返回0
        for(int i=0;i<N;i++)
        {
            if(oper[i]=='/')
            {  
               number[i+1]=(number[i])/(number[i+1]);
               oper[i]='+';
               number[i]=0;
            }
        }
        for(int i=0;i<N;i++)
        {
            if(oper[i]=='*')
            {  
               number[i+1]=(number[i])*(number[i+1]);
               oper[i]='+';
               number[i]=0;
            }
        }
        float sum=number[0];
        for(int i=0;i<(N-1);i++)
        {
            if(oper[i]=='+')
            {  
               sum=sum+number[i+1];
            }
            else
            {
               sum=sum-number[i+1]; 
            }
        }
        if(dd==sum)
        {
            n=1;
            cout<<"正确！";
        }
        else
        {
            cout<<"错误！";
        }
        cout<<endl;
        return n;
}
