# collab-practical
Insertion and Deletion in Array Using Functions
#include<stdio.h>
#define MAX 100

int a[MAX],n;

void insert(){
    int p,v;
    printf("Enter position and value: ");
    scanf("%d%d",&p,&v);
    if(n>=MAX){ printf("Full\n"); return; }
    for(int i=n;i>=p;i--) a[i]=a[i-1];
    a[p-1]=v; n++;
}

void del(){
    int p;
    printf("Enter position to delete: ");
    scanf("%d",&p);
    for(int i=p-1;i<n-1;i++) a[i]=a[i+1];
    n--;
}

void display(){
    for(int i=0;i<n;i++) printf("%d ",a[i]);
    printf("\n");
}

int main(){
    int i;
    printf("Enter size: ");
    scanf("%d",&n);
    printf("Enter elements:\n");
    for(i=0;i<n;i++) scanf("%d",&a[i]);

    insert();
    display();
    del();
    display();

    return 0;
}
 Array Implementation of Stack

#include<stdio.h>
int stack[100],n,top=-1;
void push(){
    int x;
    if(top>=n-1) printf("Overflow\n");
    else{
        scanf("%d",&x);
        stack[++top]=x;
    }
}

void pop(){
    if(top<0) printf("Underflow\n");
    else printf("Popped %d\n",stack[top--]);
}

void display(){
    for(int i=top;i>=0;i--) printf("%d ",stack[i]);
    printf("\n");
}

int main(){
    int ch;
    scanf("%d",&n);

    do{
        scanf("%d",&ch);
        if(ch==1) push();
        else if(ch==2) pop();
        else if(ch==3) display();
    }while(ch!=4);

    return 0;
}
 Singly Linked List (Insert, Delete, Display)#include<stdio.h>
#include<stdlib.h>

struct Node{
    int data;
    struct Node* next;
};

void beg(struct Node** h,int x){
    struct Node* n=malloc(sizeof(struct Node));
    n->data=x; n->next=*h; *h=n;
}

void end(struct Node** h,int x){
    struct Node* n=malloc(sizeof(struct Node));
    n->data=x; n->next=NULL;
    if(!*h){ *h=n; return; }
    struct Node* t=*h;
    while(t->next) t=t->next;
    t->next=n;
}

void delFirst(struct Node** h){
    if(!*h) return;
    struct Node* t=*h;
    *h=t->next;
    free(t);
}

void display(struct Node* h){
    while(h){ printf("%d->",h->data); h=h->next; }
    printf("NULL\n");
}

int main(){
    struct Node* head=NULL;

    beg(&head,10);
    end(&head,20);
    end(&head,30);

    display(head);

    delFirst(&head);
    display(head);

    return 0;
}
}
    Insertion Sort#include<stdio.h>

int main(){
    int a[100],n,i,j,temp;

    scanf("%d",&n);
    for(i=0;i<n;i++) scanf("%d",&a[i]);

    for(i=1;i<n;i++){
        temp=a[i];
        j=i-1;
        while(j>=0 && a[j]>temp){
            a[j+1]=a[j];
            j--;
        }
        a[j+1]=temp;
    }

    for(i=0;i<n;i++) printf("%d ",a[i]);

    return 0;
}
Binary Search
#include<stdio.h>
int main(){
    int a[100],n,x,l=0,h,m,f=0;

    scanf("%d",&n);
    for(int i=0;i<n;i++) scanf("%d",&a[i]);

    scanf("%d",&x);
    h=n-1;

    while(l<=h){
        m=(l+h)/2;
        if(a[m]==x){
            printf("Found at %d",m+1);
            f=1; break;
        }
        else if(a[m]<x) l=m+1;
        else h=m-1;
    }

    if(!f) printf("Not found");

    return 0;
}
 Binary Search Tree + Traversals
#include<stdio.h>
#include<stdlib.h>

struct Node{
    int data;
    struct Node *l,*r;
};

struct Node* insert(struct Node* t,int x){
    if(!t){
        t=malloc(sizeof(struct Node));
        t->data=x; t->l=t->r=NULL;
        return t;
    }
    if(x<t->data) t->l=insert(t->l,x);
    else t->r=insert(t->r,x);
    return t;
}

void pre(struct Node* t){
    if(t){ printf("%d ",t->data); pre(t->l); pre(t->r); }
}

void in(struct Node* t){
    if(t){ in(t->l); printf("%d ",t->data); in(t->r); }
}

void post(struct Node* t){
    if(t){ post(t->l); post(t->r); printf("%d ",t->data); }
}

int main(){
    struct Node* root=NULL;
    int a[]={1,2,3,4,5};

    for(int i=0;i<5;i++) root=insert(root,a[i]);

    pre(root);
    printf("\n");
    in(root);
    printf("\n");
    post(root);

    return 0;
}
