/*A Dictionary stores keywords and its meanings. Provide facility for adding new keywords, deleting keywords, updating values of any entry. Provide facility to display whole data sorted in ascending/ Descending order. Also find how many maximum comparisons may require for finding any keyword. Use Height balance tree and find the complexity for finding a keyword*/



#include<iostream>

#include<string.h>

using namespace std;



struct word

{

    char key[15];

    char meaning[20];



};



struct node

{

    word data;

    node *left,*right;

  };



class AVL

{

	public:

    node *root;

    

   AVL()

    {

        root=NULL;

    }

    

    node * create();

    node *insert(node *,word);

    void inorder(node *);

    node *rotateright(node *);

    node *rotateleft(node *);

    node *rr(node *);

    node *ll(node *);

    node *lr(node *);

    node *rl(node *);

    int bf(node *t);

 

};



node * AVL::create()

     {

     	int n1,i;

     	word x;

     	cout<<"\n Enter how many nodes you want to insert: ";

            cin>>n1;

            for(i=0;i<n1;i++)

            {

                cout<<"\n Enter word And meaning: \n";

                cin>>x.key>>x.meaning;

                root=insert(root,x);

            }

     return root;   

    }



node *AVL::insert(node *t,word x)

{

    if(t==NULL)

    {

        t=new node;

        t->data=x;

        t->left=NULL;

        t->right=NULL;



    }

    else

        if(strcmp(x.key,t->data.key)>0)

        {

            t->right=insert(t->right,x);

            if(bf(t)==-2)

                if(strcmp(x.key,t->right->data.key)>0)

                    t=rr(t);

                else

                    t=rl(t);



        }

        else

            if(strcmp(x.key,t->data.key)<0)

        {

            t->left=insert(t->left,x);

            if(bf(t)==2)

                if(strcmp(x.key,t->left->data.key)<0)

                    t=ll(t);

                else

                    t=lr(t);

        }

    return t;

}



node *AVL::rotateright(node *x)

{

    node *y;

    y=x->left;

    x->left=y->right;

    y->right=x;

  

    return(y);

}



node *AVL::rotateleft(node *x)

{

    node *y;

        y=x->right;

        x->right=y->left;

        y->left=x;

     

        return(y);

}



node *AVL::rr(node *t)

{

    t=rotateleft(t);

    return(t);



}



node *AVL::ll(node *t)

{

    t=rotateright(t);

    return(t);



}



node *AVL::lr(node *t)

{

    t->left=rotateleft(t->left);

    t=rotateright(t);

    return(t);

}



node *AVL::rl(node *t)

{

    t->right=rotateright(t->right);

    t=rotateleft(t);

    return(t);

}



int AVL::bf(node *t)

{

    int lh,rh;

    if(t==NULL)

        return 0;

    if(t->left==NULL)

        lh=0;

    else

        lh=1+lh;

    if(t->right==NULL)

        rh=0;

    else

        rh=1+rh;



        return(lh-rh);



}

void AVL::inorder(node *t)

{

    if(t!=NULL)

    {

        inorder(t->left);

        cout<<" ("<<t->data.key<<"  ---  "<<t->data.meaning<<") ";

        inorder(t->right);

    }

}





int main()

{

    AVL a;

    char ans;

    int op,n,n1,i;

    word x;

    do

    {

        cout<<"\n    MAIN MENU    ";

        cout<<"\n1. create";

        cout<<"\n2. display";

        cout<<"\n3. exit";

        cout<<"\n Enter your choice: ";

        cin>>op;

        switch(op)

        {

        case 1:

           a.root= a.create();

            break;

        case 2:

            cout<<"\n Inorder Sequence: \n";

            a.inorder(a.root);

            break;

        case 3:

            return 0;



        }

        cout<<"\n\n want to continue (y/n): ";

        cin>>ans;



    }while(ans=='y');

    return 0;



}