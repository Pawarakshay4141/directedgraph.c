# directedgraph.c





[5:05 pm, 05/05/2023] Akshay Pawar: #include<stdio.h>
#include<stdlib.h>
#define SIZE 10
#define NEWNODE (struct node *)malloc(sizeof(struct node))
struct node
{
int vertex;
struct node *next;
};
struct node *AList[SIZE],*IAList[SIZE];
int nov;
int noe;
void init(struct node *L[])
{
int i;
for( i=0; i<SIZE; i++)
{
L[i] = NULL;
}
}
void add_in_list(struct node *L[],int i, int v)
{
struct node *t, *l;
t = NEWNODE;
t->vertex = v;
t->next =NULL;
[5:06 pm, 05/05/2023] Akshay Pawar: if(L[i]==NULL)
{
L[i] = t;
}
else
{
t->next = L[i];
L[i] = t;
}
}
void free_list(struct node *L[])
{
int i;
struct node *s, *t;
for( i=0; i<nov; i++)
{
s=L[i];
while(s != NULL )
{
t = s;
s = s->next;
free(t);
}
L[i] = NULL;
}
}
void accept()
{
int i,j,k;
printf("How many Vertices : ");
scanf("%d", &nov);
printf("How many Edges : ");
scanf("%d", &noe);
[5:06 pm, 05/05/2023] Akshay Pawar: for(k=1; k<=noe; k++)
{
printf("Enter Edge (Vi,Vj) : ");
scanf("%d %d", &i,&j);
add_in_list(AList,i,j);
add_in_list(IAList,j,i);
}
}
void display(struct node *L[])
{
int i;
struct node *t;
for( i=0; i < nov; i++ )
{
printf("V%d -> ", i);
for( t=L[i]; t!=NULL; t = t->next)
{
printf(" [%d] -> ", t->vertex);
}
printf(" NULL \n");
}
}
void display_degree(struct node *L1[], struct node *L2[])
{
int i,indegree, outdegree, total;
struct node *t;
printf("\nDegree of Each Vertex\n");
printf("--------------------------------\n");
[5:06 pm, 05/05/2023] Akshay Pawar: for( i=0; i<nov; i++)
{
outdegree = 0;
indegree = 0;
for( t = L1[i]; t!= NULL; t=t->next)
{
outdegree++;
} 
for( t = L2[i]; t!= NULL; t=t->next)
 {
 indegree++;
 } 
total = outdegree + indegree;
 printf("V%d : Indegree = %d Outdegree = %d Total Degree = %d \n", i, indegree, outdegree, total);
}
}
int main()
{
init(AList);
init(IAList);
accept();
printf("\nAdjacency List\n");
printf("----------------------\n");
display(AList);
printf("\nInverse Adjacency List\n");
 printf("-------------------------------\n");
 display(IAList);
display_degree(AList,IAList);
free_list(AList);
free_list(IAList);
return 0;
}
[5:06 pm, 05/05/2023] Akshay Pawar: sachin@tca2009:$ ./a.out
How many Vertices : 4
How many Edges : 5
Enter Edge (Vi,Vj) : 0 1
Enter Edge (Vi,Vj) : 0 2
Enter Edge (Vi,Vj) : 1 3
Enter Edge (Vi,Vj) : 3 0
Enter Edge (Vi,Vj) : 3 2
Adjacency List
----------------------
V0 -> [2] -> [1] -> NULL 
V1 -> [3] -> NULL 
V2 -> NULL 
V3 -> [2] -> [0] -> NULL 
Inverse Adjacency List
-------------------------------
V0 -> [3] -> NULL 
V1 -> [0] -> NULL 
V2 -> [3] -> [0] -> NULL 
V3 -> [1] -> NULL 
Degree of Each Vertex
--------------------------------
V0 : Indegree = 1 Outdegree = 2 Total Degree = 3 
V1 : Indegree = 1 Outdegree = 1 Total Degree = 2 
V2 : Indegree = 2 Outdegree = 0 Total Degree = 2 
V3 : Indegree = 1 Outdegree = 2 Total Degree = 3
