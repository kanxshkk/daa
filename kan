/**AVL completeo picaso *************************************************************************************************/
#include<iostream>
#include<stdlib.h>

using namespace std;

struct node
{
    int data;
    struct node * left;
    struct node * right;
}*root;

class avltree
{
public:
    int height (node * ptr);
    int bf(node * ptr);
    node * rr_rotat(node * );
    node * ll_rotat(node * );
    node * lr_rotat(node * );
    node * rl_rotat(node * );
    node * balance(node * );
    node * insert(node * , int );
    void show(node * );
    node * Delete(node *T,int x);
    void printLevelOrderBFS(node * r);
    void printGivenLevel(node * r, int level);
    avltree()
    {
        root = NULL;
    }
};

void avltree::printLevelOrderBFS(node * r) {
    int h = height(r);
    for (int i = 0; i <= h; i++)
      printGivenLevel(r, i);
}
void avltree::printGivenLevel(node * r, int level)
{
    if (r == NULL)
      return;
    else if (level == 0)
      cout << r -> data << "-> ";
    else // level > 0
    {
      printGivenLevel(r -> left, level - 1);
      printGivenLevel(r -> right, level - 1);
    }
  }

node * avltree::rr_rotat(node * parent)
{
    node * temp = parent -> right;
    parent->right= temp-> left;
    temp->left=parent;
    cout<<"Right-Right Rotation";
    return temp;
}

node * avltree::ll_rotat(node * parent)
{
    node * temp = parent -> left;
    parent->left= temp-> right;
    temp->right=parent;
    cout<<"Left-Left Rotation";
    return temp;
}

node * avltree::rl_rotat(node * parent)
{
    node * temp = parent -> right;
    parent->right= ll_rotat(temp);
    cout<<"Right-Left Rotation";
    return rr_rotat(temp);
}

node * avltree::lr_rotat(node * parent)
{
    node * temp = parent -> left;
    parent->left= rr_rotat(temp);
    cout<<"Left-Right Rotation";
    return ll_rotat(temp);
}

int avltree::height(node *ptr)
{
    int h = 0;
       if (ptr != NULL)
       {
            int l_height = height(ptr->left);
            int r_height = height(ptr->right);
            int max_height = max(l_height, r_height);
            h = max_height + 1;
       }
       return h;
}

int avltree::bf(node *ptr)
{
    int l_height = height(ptr->left);
    int r_height = height(ptr->right);
    int b_factor = l_height - r_height;
    return b_factor;
}

node * avltree::insert(node * root,int ele)
{

    if(root == NULL)
    {
        root=new node;
        root->data=ele;
        root->left=NULL;
        root->right=NULL;
        return root;
    }
    else if (ele < root->data)
    {
        root->left=insert(root->left,ele);
        root=balance(root);

    }
    else if (ele > root->data)
    {
        root->right=insert(root->right,ele);
        root=balance(root);
    }
    return root;
}

node * avltree::balance(node * ptr)
{
    int _bf=bf(ptr);
    if ( _bf>1)
    {
        if (bf(ptr->left)>0)
            ptr=ll_rotat(ptr);
        else
            ptr=lr_rotat(ptr);
    }
    else if ( _bf < -1)
    {
        if (bf(ptr-> right) >0)
            ptr=rl_rotat(ptr);
        else
            ptr=rr_rotat(ptr);
    }
    return ptr;
}

void inorder(node *t)
{
    if (t == NULL)
        return;
    inorder(t->left);
    cout << t->data << " ";
    inorder(t->right);
   }
void preorder(node *t)
{
    if (t == NULL)
        return;
    cout << t->data << " ";
    preorder(t->left);
    preorder(t->right);
}
void postorder(node *t)
{
    if (t == NULL)
        return;
    postorder(t ->left);
    postorder(t ->right);
    cout << t->data << " ";
}
void avltree::show(node * ptr)
{
    cout<<endl<<"postOrder:"<<endl;
    postorder(ptr);
    cout<<endl<<"inOrder:"<<endl;
    inorder(ptr);
    cout<<endl<<"preOrder:"<<endl;
    preorder(ptr);
    cout<<"\n\n"<<"levelOrder"<<endl;
    printLevelOrderBFS(ptr);
    cout<<endl<<endl;
}

node * avltree::Delete(node *T,int x)
/**
L(0),L(-1) RR
L(-1) RL

R(0),R(1) LL
R(-1) LR
*/
{
    node *p;

    if(T == NULL)
    {
        return NULL;
    }
    else
        if(x > T->data)
        {
            T -> right = Delete(T -> right,x);

            if(bf(T) == 2)
                if(bf(T -> left) >= 0)
                    T = ll_rotat(T);
                else
                    T = lr_rotat(T);
        }
        else
            if(x < T -> data)
            {
                T -> left = Delete(T->left,x);
                if(bf(T)==-2)
                    if(bf(T->right)<=0)
                        T=rr_rotat(T);
                    else
                        T=rl_rotat(T);
            }
            else
            {
                if(T -> right != NULL)
                {
                    p = T -> right;

                    while(p -> left != NULL)
                        p = p -> left;

                    T -> data = p -> data;
                    T -> right = Delete(T -> right,p->data);

                    if(bf(T) == 2)
                        if(bf (T -> left) >= 0)
                            T=ll_rotat(T);
                        else
                            T=lr_rotat(T);
                }
                else
                    return(T->left);
            }
    //T ->ht = height(T);
    return(T);
}

int main()
{
    int c, i ,x;
    avltree avl;
    while (1)
    {
         cout << "\n1.Insert Element into the tree" << endl;
         cout << "2.show Balanced AVL Tree" << endl;
         cout << "3.Deletion" << endl;
         cout << "4.Exit" << endl;
         cout << "Enter your Choice: ";
         cin >> c;
        switch (c)
         {
            case 1:
               cout << "Enter value to be inserted: ";
               cin >> i;
               root= avl.insert(root, i);
               avl.show(root);
               break;
            case 2:
               if (root == NULL)
               {
                  cout << "Tree is Empty" << endl;
                  continue;
               }
                  cout << "Balanced AVL Tree:" << endl;
                  avl.show(root);
                  cout<<endl;
                  break;
            case 3:
                cout << "Enter a element to be deleted : ";
                cin >> x;
                root = avl.Delete(root,x);
                break;
            case 4:
                exit(1);
                break;
            default:
               cout << "Wrong Choice" << endl;
      }
   }
   return 0;
}
