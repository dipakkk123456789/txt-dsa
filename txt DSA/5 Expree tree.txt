/*
Construct  an  expression  tree  from  the  given  prefix  expression  eg.  +--a*bc/def  and 
traverse it using post order traversal (non recursive) and then delete the entire tree. */

#include<iostream>
#include<stack>
using namespace std;

struct node
{
    char ch;
    node *cL;
    node *cR;
};

class expression
{
    public:
    char exp[20];
    stack<node *>s1;
    stack<node *>s3;
    node *root;
    void create();
    void postoder();
    void deltion();

};

void expression::create()
{
    cout<<"\n enter the expression\n";
    cin>>exp;

    node *ch1,*ch2;
    int i=0;
	while(exp[i]!='\0')
    {
        i++;
    }

    while(i>=0)
    {
        if(exp[i]=='/' || exp[i]=='*' || exp[i]=='-' || exp[i]=='+')
        {
            ch1=s1.top();
            s1.pop();
            ch2=s1.top();
            s1.pop();

            node *nnode=new node;
            nnode->ch=exp[i];
            nnode->cL=ch1;
            nnode->cR=ch2;
            s1.push(nnode);

        }
        else
        {
            node *nnode=new node;
            nnode->ch=exp[i];
            nnode->cL=NULL;
            nnode->cR=NULL;
            s1.push(nnode);

        }
        i--;
    }
}

void expression::postoder()
{
    
      stack<node *>s2;
    node *current;
    root=s1.top();
    while(!s1.empty())
    {
        current=s1.top();
        s1.pop();
        s2.push(current);
        s3.push(current);

        if(current->cL!=NULL)
         {   s1.push(current->cL);
         }
        if(current->cR!=NULL)
        {   
            s1.push(current->cR);
        }
    }
    
    while(!s2.empty())
    {
        current=s2.top();
        cout<<current->ch;
        s2.pop();
    }
      
}
void expression:: deltion()
{
    root->cL=NULL;
    root->cR=NULL;
    root=NULL;
}

int main()
{
    expression  ob;
    char c;
    int n;
        do{
    	   
        cout<<"\n 1.to create expression tree \n 2.non recursive postorder \n3.deletion of tree\n";
        cout<<"\n enter your choice=";
        cin>>n;
        switch(n)
        {
            case 1:ob.create();
                break;
            case 2:ob.postoder();
                break;  
            case 3:ob.deltion(); 
                break;       
            default:cout<<"invalid choice";
        }
      cout<<"\n do you want to continue: =";
      cin>>c;
    }while(c=='y');
    return 0;
    
}