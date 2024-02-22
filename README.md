/*1. Develop a Program in C for the following:
a) Declare a calendar as an array of 7 elements (A dynamically Created array) to represent 7 days of a 
week. Each Element of the array is a structure having three fields. The first field is the name of the Day (A 
dynamically allocated String), The second field is the date of the Day (A integer), the third field is the 
description of the activity for a particular day (A dynamically allocated String).
b) Write functions create (), read () and display (); to create the calendar, to read the data from the 
keyboard and to print weeks activity details report on screen.*/
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
// Define the structure for a day
struct Day {
char *name; // Dynamic string for day name
int date; // Integer for date
char *description; // Dynamic string for activity description
};
// Function to create the calendar
void create(struct Day calendar[7]) {
for (inti = 0; i< 7; i++) {
 // dynamically allocate memory for the day name and description
calendar[i].name = (char *)malloc(50 * sizeof(char)); // Assuming max length of day name is 50 characters
calendar[i].description = (char *)malloc(100 * sizeof(char)); // Assuming max length of description is 100 
characters
 }
}
// Function to read the weekly activity details
void read(struct Day calendar[7]) {
for (inti = 0; i< 7; i++) {
printf("Enter name for Day %d: ", i + 1);
scanf("%s", calendar[i].name);
printf("Enter date for Day %d: ", i + 1);
scanf("%d", &calendar[i].date);
printf("Enter description for Day %d: ", i + 1);
scanf("%s", calendar[i].description);
 }
}
// Function to display the weekly activity details
void display(struct Day calendar[7]) {
for (inti = 0; i< 7; i++) {
printf("Day Name: %s\n", calendar[i].name);
printf("Date: %d\n", calendar[i].date);
printf("Description: %s\n", calendar[i].description);
printf("\n");
 }
}
int main() {
struct Day calendar[7];
 // Call the create function to create the calendar
create(calendar);
read(calendar);
 // Display the weekly activity details
printf("\nWeekly Activity Details:\n");
display(calendar);
 // Free dynamically allocated memory
for (inti = 0; i< 7; i++) {
free(calendar[i].name);
free(calendar[i].description);
 }
return 0;
}
2. Develop a Program in C for the following operations on Strings.
a. Read a main String (STR), a Pattern String (PAT) and a Replace String (REP)
b. Perform Pattern Matching Operation: Find and Replace all occurrences of PAT in
STR with REP if PAT exists in STR. Report suitable messages in case PAT does not
exist in STR
Support the program with functions for each of the above operations. Don't use Built-in
functions.
#include<stdio.h>
void read_string();
void pattern_match();
char STR[100],PAT[100],REP[100],ans[100];
int i,j,c,m,k,flag=0;
int main()
{
read_string();
pattern_match();
return 0;
}
void read_string()
{
printf("\nEnter the MAIN string: \n");
gets(STR);
printf("\nEnter a PATTERN string: \n");
gets(PAT);
printf("\nEnter a REPLACE string: \n");
gets(REP);
}
void pattern_match()
{
i= m=c=j=0;
while ( STR[c] != '\0')
{
// Checking for Match
if ( STR[m] == PAT[i] )
{
i++;
m++;
flag=1;
if ( PAT[i] == '\0')
{
//replace string in ans string
for(k=0; REP[k] != '\0';k++,j++)
ans[j] = REP[k];
i=0;
c=m;
}
}
else //mismatch
{
ans[j] = STR[c];
j++;
c++;
m = c;
i=0;
}
}
if(flag==0)
{
printf("Pattern doesn't found!!!");
}
else
{ ans[j] ='\0';
printf("\nThe RESULTANT string is:%s\n" ,ans);
}
}
3. Develop a menu driven Program in C for the following operations on STACK of Integers
(Array Implementation of Stack with maximum size MAX)
a. Push an Element on to Stack
b. Pop an Element from Stack
c. Demonstrate how Stack can be used to check Palindrome
d. Demonstrate Overflow and Underflow situations on Stack
e. Display the status of Stack
f. Exit
Support the program with appropriate functions for each of the above operations
#include <stdio.h>
#include <stdlib.h>
int stack[6],rev[6];
int top=-1,k=0;
int size;
void push();
void pop();
void display();
int pali();
void main()
{
int choice,f;
printf("Enter the size for stack\n");
scanf("%d",&size);
printf("1.Push\n2.Pop\n3.Display\n4.Check for Palindrome\n5.Exit\n");
while(1)
{
printf("Enter the choice\n");
scanf("%d",&choice);
switch(choice)
{
case 1:push();
break;
case 2:pop();
break;
case 3:display();
break;
case 4:f=pali();
if(f==1)
printf("It's Palindrome\n");
else
printf("It's not a Palindrome\n");
break;
case 5:exit(0);
default:printf("Wrong choice...\n");
}
}
}
void push()
{
int num;
if(top==(size-1))
{
printf("Stack Overflow\n");
}
else
{
printf("Enter the number to be pushed\n");
scanf("%d",&num);
top++;
stack[top]=num;
}
}
void pop()
{
int num;
if(top==-1)
{
printf("Stack Underflow\n");
}
else
{
num=stack[top];
printf("Popped element is %d\n",num);
top--;
}
}
void display()
{
int i;
if(top==-1)
{
printf("Stack Underflow\n");
}
else
{
printf("Stack Contents....\n");
for(i=top;i>=0;i--)
{
printf("%d\n",stack[i]);
rev[k++]=stack[i];
}
}
}
int pali()
{
int i,flag=1;
for(i=top;i>=0;i--)
{
if(stack[i]!=rev[--k])
{
flag=0;
}
}
return flag;
}
4. Develop a Program in C for converting an Infix Expression to Postfix Expression. Program
should support for both parenthesized and free parenthesized
expressions
#define size 50 /* size of stack */
#include <ctype.h>
#include <stdio.h>
char s[size];
int top = -1; /* global declarations */
void push(char elem) /* function for push operation */
{
s[++top] = elem;
}
char pop() /* function for pop operation */
{
return (s[top--]);
}
int pr(char elem) /* function for precedence */
{
switch (elem)
{
case '#':
return 0;
case '(':
return 1;
case '+':
case '-':
return 2;
case '*':
case '/':
case '%':
return 3;
case '^':
return 4;
} }
void main() /* main program */
{
char infx[50], pofx[50], ch, elem;
int i = 0, k = 0;
printf("\n\nEnter the infix expression ");
scanf("%s", infx);
push('#');
while ((ch = infx[i++]) != '\0')
{
if (ch == '(')
push(ch);
else if (isalnum(ch))
pofx[k++] = ch;
else if (ch == ')')
{
while (s[top] != '(')
{
pofx[k++] = pop();
}
elem = pop(); /* remove ( */
}
else /* operator */
{
while (pr(s[top]) >= pr(ch))
{
pofx[k++] = pop();
}
push(ch);
}
}
while (s[top] != '#') /* pop from stack till empty */
{
pofx[k++] = pop();
}
pofx[k] = '\0'; /* make pofx as valid string */
printf("\n\n Given infix expression: %s\n postfix expression is: %s\n", infx, pofx);
}
5. Develop a Program in C for the following Stack Applications
a. Evaluation of Suffix expression with single digit operands and operators: +, -, *, /, %, ^
b. Solving Tower of Hanoi problem with n disks
Program (5-A)
#include<ctype.h>
#include <stdio.h>
float stack[20];
int top=-1;
float eval_postfix(char[]); // function to evalute an given expression
void push(float); // function to push elements to stack 
float pop(); // function to pop the elements from the stack
main()
{
char postfix[20];
float result;
printf("enter postfix expr\n");
scanf("%s", postfix);
result=eval_postfix(postfix);
printf("The result = %f\n",result);
}
float eval_postfix(char postfix[])
{
int i=0,k;
char ch,op1,op2;
float res;
while(postfix[i]!='\0') //check till the end of string
{
ch=postfix[i];
if(isdigit(ch)) //check for digitschecks whether a character is numeric (0-9) or not. 
{
k=ch-'0'; 
push(k);
}
else
{
op2=pop();
op1=pop();
switch(ch)
{
case '+':push(op1+op2);
break;
case '-':push(op1-op2);
break;
case '*':push(op1*op2);
break;
case '/':push(op1/op2);
break;
case '^':push(pow(op1,op2));
break;
default :printf("illegal\n");
exit(0);
}
}
i++;
}
res=pop();
if(top!=-1)
{
printf("not a valid expression");
exit(1);
}
return(res);
}
void push(float num)
{ 
top++;
stack[top]=num;
return;
}
float pop()
{
float num;
if(top == -1)
{
printf("not a valid");
exit(0);
}
else
{
num=stack[top];
top--;
return(num);
}
}
Program (5-B)
Towers of Hanoi
#include <stdio.h> 
void towers(int, char, char, char); 
int main() 
{ 
int num; 
printf("Enter the number of disks : "); 
scanf("%d", &num); 
printf("The sequence of moves involved in the Tower of Hanoi are :\n"); 
towers(num, 'A', 'C', 'B'); 
return 0; 
} 
void towers(int num, char frompeg, char topeg, char auxpeg) 
{ 
if (num == 1) 
{ 
printf("\n Move disk 1 from peg %c to peg %c", frompeg, topeg); 
return; 
} 
towers(num - 1, frompeg, auxpeg, topeg); 
printf("\n Move disk %d from peg %c to peg %c", num, frompeg, topeg); 
towers(num - 1, auxpeg, topeg, frompeg); 
}
6. Develop a menu driven Program in C for the following operations on Circular QUEUE of
Characters (Array Implementation of Queue with maximum size MAX)
a. Insert an Element on to Circular QUEUE
b. Delete an Element from Circular QUEUE
c. Demonstrate Overflow and Underflow situations on Circular QUEUE
d. Display the status of Circular QUEUE
e. Exit
Support the program with appropriate functions for each of the above operations
#include <string.h>
#include <stdio.h>
#define SIZE 3
char CQ[SIZE];
int front=-1, rear=-1;
int ch;
void CQ_Insert();
void CQ_Delet();
void CQ_Display();
void main()
{
printf("1.Insert\n2.Delete\n3.Display\n4.Exit\n");
while(1)
{
printf("Enter your choice\n");
scanf("%d",&ch);
switch(ch)
{
case 1: CQ_Insert();
break;
case 2:CQ_Delet();
break;
case 3:CQ_Display();
break;
case 4: exit(0);
}
}
}
void CQ_Insert()
{
char ele;
if(front==(rear+1)%SIZE)
{
printf("Circular Queue Full\n");
return;
}
if(front==-1)
front++;
printf("Enter the element to be inserted\n");
scanf("\n%c",&ele);
rear = (rear+1)%SIZE;
CQ[rear] =ele;
}
void CQ_Delet()
{
char item;
if(front == -1)
{
printf("Circular Queue Empty\n");
return;
}
else if(front == rear)
{
item=CQ[front];
printf("Deleted element is: %c\n",item);
front=-1;
rear=-1;
}
else
{
item =CQ[front];
printf("Deleted element is: %c\n",item);
front = (front+1)%SIZE;
}
}
void CQ_Display()
{
int i;
if(front==-1)
printf("Circular Queue is Empty\n");
else
{
printf("Elements of the circular queue are..\n");
for(i=front;i!=rear;i=(i+1)%SIZE)
{
printf("%c\t",CQ[i]);
}
printf("%c\n",CQ[i]);
}
}
7. Develop a menu driven Program in C for the following operations on Singly Linked List
(SLL) of Student Data with the fields: USN, Name, Programme, Sem, PhNo
a. Create a SLL of N Students Data by using front insertion.
b. Display the status of SLL and count the number of nodes in it
c. Perform Insertion / Deletion at End of SLL
d. Perform Insertion / Deletion at Front of SLL(Demonstration of stack)
e. Exit
#include <stdio.h>
#include<stdlib.h>
#include<string.h>
int count=0;
struct stud
{
long long int ph;
int sem;
char name[15],usn[15],brnch[8];
struct stud *next;
}*head=NULL,*tail=NULL,*temp=NULL,*temp1;
void create(long long int n,int s,char na[20],char u[15],char b[5])
{
if(head==NULL)
{
head=(struct stud*)malloc(1*sizeof(struct stud));
head->ph=n;
head->sem=s;
strcpy(head->name,na);
strcpy(head->usn,u);
strcpy(head->brnch,b);
head->next=NULL;
tail=head;
count++;
}
else
{
temp=(struct stud*)malloc(1*sizeof(struct stud));
temp->ph=n;
temp->sem=s;
strcpy(temp->name,na);
strcpy(temp->usn,u);
strcpy(temp->brnch,b);
temp->next=NULL;
tail->next=temp;
tail=temp;
count++;
}
}
void display()
{
temp1=head;
if(temp1==NULL)
{
printf("\nlist is empty\n");
}
else
{
printf("student details are as follows:\n");
while(temp1!=NULL)
{
printf("-----------------------\n");
printf("NAME:%s\nUSN:%s\nBRANCH:%s\nSEM:%d\nPHONE NO.:%lld\n",temp1->name,temp1-
>usn,temp1->brnch,temp1->sem,temp1->ph);
printf("-----------------------\n");
temp1=temp1->next;
}
printf("no. of nodes=%d\n",count);
}
}
void insert_head(long long int n,int s,char na[15],char u[15],char b[8])
{
temp=(struct stud*)malloc(1*sizeof(struct stud));
temp->ph=n;
temp->sem=s;
strcpy(temp->name,na);
strcpy(temp->usn,u);
strcpy(temp->brnch,b);
temp->next=head;
head=temp;
count++;
}
void insert_tail(long long int n,int s,char na[15],char u[15],char b[8])
{
temp=(struct stud*)malloc(1*sizeof(struct stud));
temp->ph=n;
temp->sem=s;
strcpy(temp->name,na);
strcpy(temp->usn,u);
strcpy(temp->brnch,b);
tail->next=temp;
temp->next=NULL;
tail=temp;
count++;
}
void delete_head()
{
temp1=head;
if(temp1==NULL)
{
printf("list is empty\n");
}
else
{
head=head->next;
printf("deleted node is:\n");
printf("-----------------------\n");
printf("NAME:%s\nUSN:%s\nBRANCH:%s\nSEM:%d\nPHONE NO.:%lld\n",temp1->name,temp1-
>usn,temp1->brnch,temp1->sem,temp1->ph);
printf("-----------------------\n");
free(temp1);
count--;
}
}
void delete_tail()
{
temp1=head;
if(temp1==NULL)
{
printf("list is empty\n");
}
while(temp1->next!=tail)
{
temp1=temp1->next;
}
printf("deleted node is:\n");
printf("-----------------------\n");
printf("NAME:%s\nUSN:%s\nBRANCH:%s\nSEM:%d\nPHONE NO.:%lld\n",tail->name,tail->usn,tail-
>brnch,tail->sem,tail->ph);
printf("-----------------------\n");
free(tail);
tail=temp1;
tail->next=NULL;
count--;
}
void main()
{
int choice;
long long int ph;
int sem;
char name[20],usn[15],brnch[5];
printf("--------MENU----------\n");
printf("1.create\n2.Insert from head\n3.Insert from tail\n4.Delete from head\5.Delete from 
tail\n6.display\n7.exit\n");
printf("----------------------\n");
while(1)
{
printf("enter your choice\n");
scanf("%d",&choice);
switch(choice)
{
case 1:printf("enter the name usn branch sem phno. of the student respectively\n");
 scanf("%s%s%s%d%lld",name,usn,brnch,&sem,&ph);
 create(ph,sem,name,usn,brnch);
 break;
case 2: printf("enter the name usn branch sem phno. of the student respectively\n");
 scanf("%s%s%s%d%lld",name,usn,brnch,&sem,&ph);
 insert_head(ph,sem,name,usn,brnch);
 break;
case 3: printf("enter the name usn branch sem phno. of the student respectively\n");
 scanf("%s%s%s%d%lld",name,usn,brnch,&sem,&ph);
 insert_tail(ph,sem,name,usn,brnch);
 break;
case 4:delete_head();
 break;
case 5:delete_tail();
 break;
case 6:display();
 break;
case 7: exit(0);
default:printf("invalid option\n");
}
}
}
8. Develop a menu driven Program in C for the following operations on Doubly Linked List
(DLL) of Employee Data with the fields: SSN, Name, Dept, Designation,
Sal, PhNo
a. Create a DLL of N Employees Data by using end insertion.
b. Display the status of DLL and count the number of nodes in it
c. Perform Insertion and Deletion at End of DLL
d. Perform Insertion and Deletion at Front of DLL
e. Demonstrate how this DLL can be used as Double Ended Queue.
f. Exit
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct Enode
{
char ssn[15];
char name[20];
char dept[5];
char designation[10];
int salary;
long long int phno;
struct Enode *left;
struct Enode *right;
}*head=NULL;
struct Enode *tail,*temp1,*temp2;
void create(char [],char [],char [],char [],int ,long long int);
void ins_beg(char [],char [],char [],char [],int ,long long int);
void ins_end(char [],char [],char [],char [],int ,long long int);
void del_beg();
void del_end();
void display();
int count=0;
void main()
{
int choice;
char s[15],n[20],dpt[5],des[10];
int sal;
long long int p;
printf("1.Create\n2.Display\n3.Insert at beginning\n4.Insert at End\n5.Delete at beginning\n6.Delete at 
End\n7.Exit\n");
while(1)
{
printf("\nEnter your choice\n");
scanf("%d",&choice);
switch(choice)
{
case 1: printf("Enter the required data(Emp no,Name,Dept,Desig,sal,phone\n");
scanf("%s%s%s%s%d%lld",s,n,dpt,des,&sal,&p);
create(s,n,dpt,des,sal,p);
break;
case 2: display();
break;
case 3:printf("Enter the required data (Emp no,Name,Dept,Desig,sal,phone\n");
scanf("%s%s%s%s%d%lld",s,n,dpt,des,&sal,&p);
ins_beg(s,n,dpt,des,sal,p);
break;
case 4: printf("Enter the required data(Emp no,Name,Dept,Desig,sal,phone\n");
scanf("%s%s%s%s%d%lld",s,n,dpt,des,&sal,&p);
ins_end(s,n,dpt,des,sal,p);
break;
case 5: del_beg();
break;
case 6: del_end();
break;
case 7: exit(0);
}
}
}
void create(char s[15],char n[20],char dpt[5],char des[10],int sal,long long int p)
{
if(head==NULL)
{
head=(struct Enode *)malloc(1*sizeof(struct Enode));
strcpy(head->ssn,s);
strcpy(head->name,n);
strcpy(head->dept,dpt);
strcpy(head->designation,des);
head->salary=sal;
head->phno=p;
head->left=NULL;
head->right=NULL;
tail=head;
}
else
{
temp1=(struct Enode *)malloc(1*sizeof(struct Enode));
strcpy(temp1->ssn,s);
strcpy(temp1->name,n);
strcpy(temp1->dept,dpt);
strcpy(temp1->designation,des);
temp1->salary=sal;
temp1->phno=p;
tail->right=temp1;
temp1->right=NULL;
temp1->left=tail;
tail=temp1;
}
}
void display()
{
temp1=head;
printf("Employee Details ......\n");
while(temp1!=NULL)
{
printf("------------------\n");
printf("%s\n%s\n%s\n%s\n%d\n%lld\n",temp1->ssn,temp1->name,temp1->dept,temp1->designation,temp1-
>salary,temp1->phno);
printf("------------------");
temp1=temp1->right;
}
}
void ins_beg(char s[15],char n[20],char dpt[5],char des[10],int sal,long long int p)
{
temp1=(struct Enode *)malloc(1*sizeof(struct Enode));
strcpy(temp1->ssn,s);
strcpy(temp1->name,n);
strcpy(temp1->dept,dpt);
strcpy(temp1->designation,des);
temp1->salary=sal;
temp1->phno=p;
temp1->right=head;
head->left=temp1;
head=temp1;
temp1->left=NULL;
}
void ins_end(char s[15],char n[20],char dpt[5],char des[10],int sal,long long int p)
{
temp1=(struct Enode *)malloc(1*sizeof(struct Enode));
strcpy(temp1->ssn,s);
strcpy(temp1->name,n);
strcpy(temp1->dept,dpt);
strcpy(temp1->designation,des);
temp1->salary=sal;
temp1->phno=p;
tail->right=temp1;
temp1->left=tail;
temp1->right=NULL;
tail=temp1;
}
void del_beg()
{
temp1=head->right;
free(head);
head=temp1;
head->left=NULL;
}
void del_end()
{
temp1=tail->left;
free(tail);
tail=temp1;
tail->right=NULL;
}
9. Develop a Program in C for the following operationson Singly Circular Linked List (SCLL)
with header nodes
a. Represent and Evaluate a Polynomial P(x,y,z) = 6x2y2z-4yz5+3x3yz+2xy5z-2xyz3
b. Find the sum of two polynomials POLY1(x,y,z) and POLY2(x,y,z) and store the
result in POLYSUM(x,y,z)
Support the program with appropriate functions for each of the above operations
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
struct node{
int coeff;
int expo;
struct node *ptr;
};
struct node *head1,*head2,*head3, *temp,*temp1,*temp2,*temp3,*list1,*list2,*list3,*list;
struct node *dummy1,*dummy2,*dummy3;
struct node * create_poly(int , int, struct node *);
//void create_poly2(int , int);
void display(struct node *);
void add_poly();
void eval_poly(int );
int n,ch;
int c,e,i;
void main()
{
int x;
list1=list2=list3=NULL;
printf("1.Create first polynomial\n2.Create Second Polynomial\n3.Display both the polynomials\n");
printf("4.Add Polynomials\n5.Evaluate a Polynomial\n6.Exit\n");
while(1)
{
printf("Enter choice\n");
scanf("%d",&ch);
switch(ch)
{
case 1: printf("Enter the number of terms\n");
scanf("%d",&n);
printf("Enter coefficient & power of each term\n");
for(i=0;i<n;i++)
{
scanf("%d%d",&c,&e);
list1=create_poly(c,e,list1);
}
break;
case 2: printf("Enter the number of terms\n");
scanf("%d",&n);
printf("Enter coefficient & power of each term\n");
for(i=0;i<n;i++)
{
scanf("%d%d",&c,&e);
list2=create_poly(c,e,list2);
}
break;
case 3: display(list1);
display(list2);
break;
case 4: add_poly();
display(list3);
break;
case 5:printf("Enter the value for x\n");
scanf("%d",&x);
eval_poly(x);
break;
case 6:exit(0);
}
}
}
struct node * create_poly(int c, int e, struct node *list)
{
if(list==NULL)
{
dummy1=(struct node*)malloc(1*sizeof(struct node));
dummy1->coeff=0;
dummy1->expo=0;
dummy1->ptr=list1;
list=(struct node*)malloc(1*sizeof(struct node));
list->coeff=c;
list->expo=e;
//list1->ptr=list1;
head1=list;
head1->ptr=dummy1;
}
else
{
temp=(struct node*)malloc(1*sizeof(struct node));
temp->coeff=c;
temp->expo=e;
head1->ptr=temp;
temp->ptr=dummy1;
head1=temp;
}
return list;
}
void add_poly()
{
if(list3==NULL)
{
dummy3=(struct node*)malloc(1*sizeof(struct node));
dummy3->coeff=0;
dummy3->expo=0;
dummy3->ptr=list3;
temp1=list1;
temp2=list2;
}
while((temp1->coeff!=0)&&(temp2->coeff!=0))
{
temp=(struct node*)malloc(1*sizeof(struct node));
if(list3==NULL)
{
list3=temp;
head3=list3;
}
if(temp1->expo==temp2->expo)
{
temp->coeff=temp1->coeff+temp2->coeff;
temp->expo=temp1->expo;
head3->ptr=temp;
head3=temp;
head3->ptr=dummy3;
temp1=temp1->ptr;
temp2=temp2->ptr;
}
else if(temp1->expo>temp2->expo)
{
temp->coeff=temp1->coeff;
temp->expo=temp1->expo;
head3->ptr=temp;
head3=temp;
head3->ptr=dummy3;
temp1=temp1->ptr;
}
else
{
temp->coeff=temp2->coeff;
temp->expo=temp2->expo;
//temp->ptr=list3;
head3->ptr=temp;
head3=temp;
head3->ptr=dummy3;
//head3=temp;
temp2=temp2->ptr;
}
}
if(temp1->coeff==0)
{
while(temp2->coeff!=0)
{
temp=(struct node*)malloc(1*sizeof(struct node));
temp->coeff=temp2->coeff;
temp->expo=temp2->expo;
head3->ptr=temp;
head3=temp;
head3->ptr=dummy3;
//head3=temp;
temp2=temp2->ptr;
}
}
if(temp2->coeff==0)
{
while(temp1->coeff!=0)
{
temp=(struct node*)malloc(1*sizeof(struct node));
temp->coeff=temp1->coeff;
temp->expo=temp1->expo;
head3->ptr=temp;
head3=temp;
head3->ptr=dummy3;
//head3=temp;
temp1=temp1->ptr;
}
}
}
void display(struct node *list)
{
temp=list;
printf("\nPOLYNOMIAL: ");
while(temp->coeff!=0)
{
printf("%dX^%d+",temp->coeff,temp->expo);
temp=temp->ptr;
}
printf("\n");
}
void eval_poly(int x)
{
int result=0;
temp1=list1;
temp2=list2;
while(temp1->coeff!=0)
{
result+=(temp1->coeff)*pow(x,temp1->expo);
temp1=temp1->ptr;
}
printf("Polynomial 1 Evaluation:%d\n",result);
result=0;
while(temp2->coeff!=0)
{
result+=(temp2->coeff)*pow(x,temp2->expo);
temp2=temp2->ptr;
}
printf("Polynomial 2 Evaluation:%d\n",result);
}
10. Develop a menu driven Program in C for the following operations on Binary Search Tree
(BST) of Integers .
a. Create a BST of N Integers: 6, 9, 5, 2, 8, 15, 24, 14, 7, 8, 5, 2
b. Traverse the BST in Inorder, Preorder and Post Order
c. Search the BST for a given element (KEY) and report the appropriate message
d. Exit
#include <stdio.h>
#include <stdlib.h>
struct BST
{
int data;
struct BST *left;
struct BST *right;
};
typedef struct BST NODE;
NODE *node;
NODE* createtree(NODE *node, int data)
{
if (node == NULL)
{
NODE *temp;
temp= (NODE*)malloc(sizeof(NODE));
temp->data = data;
temp->left = temp->right = NULL;
return temp;
}
if (data < (node->data))
{
node->left = createtree(node->left, data);
}
else if (data > node->data)
{
node -> right = createtree(node->right, data);
}
return node;
}
NODE* search(NODE *node, int data)
{
if(node == NULL)
printf("\nElement not found");
else if(data < node->data)
{
node->left=search(node->left, data);
}
else if(data > node->data)
{
node->right=search(node->right, data);
}
else
printf("\nElement found is: %d", node->data);
return node;
}
void inorder(NODE *node)
{
if(node != NULL)
{
inorder(node->left);
printf("%d\t", node->data);
inorder(node->right);
}
}
void preorder(NODE *node)
{
if(node != NULL)
{
printf("%d\t", node->data);
preorder(node->left);
preorder(node->right);
}
}
void postorder(NODE *node)
{
if(node != NULL)
{
postorder(node->left);
postorder(node->right);
printf("%d\t", node->data);
}
}
NODE* findMin(NODE *node)
{
if(node==NULL)
{
return NULL;
}
if(node->left)
return findMin(node->left);
else
return node;
}
NODE* del(NODE *node, int data)
{
NODE *temp;
if(node == NULL)
{
printf("\nElement not found");
}
else if(data < node->data)
{
node->left = del(node->left, data);
}
else if(data > node->data)
{
node->right = del(node->right, data);
}
else
{ 
/* Now We can delete this node and replace with either minimum element in the right sub tree or maximum 
element in the left subtree */
if(node->right && node->left)
{ 
/* Here we will replace with minimum element in the right sub tree */
temp = findMin(node->right);
node -> data = temp->data;
/* As we replaced it with some other node, we have to delete that node */
node -> right = del(node->right,temp->data);
}
else
{
/* If there is only one or zero children then we can directly remove it from the tree and connect its parent to its 
child */
temp = node;
if(node->left == NULL)
node = node->right;
else if(node->right == NULL)
node = node->left;
free(temp); /* temp is longer required */
}
}
return node;
}
void main()
{
int data, ch, i, n;
NODE *root=NULL;
clrscr();
while (1)
{
printf("\n1.Insertion in Binary Search Tree");
printf("\n2.Search Element in Binary Search Tree");
printf("\n3.Delete Element in Binary Search Tree");
printf("\n4.Inorder\n5.Preorder\n6.Postorder\n7.Exit");
printf("\nEnter your choice: ");
scanf("%d", &ch);
switch (ch)
{
case 1: printf("\nEnter N value: " );
scanf("%d", &n);
printf("\nEnter the values to create BST like(6,9,5,2,8,15,24,14,7,8,5,2)\n");
for(i=0; i<n; i++)
{
scanf("%d", &data);
root=createtree(root, data);
}
break;
case 2: printf("\nEnter the element to search: ");
scanf("%d", &data);
root=search(root, data);
break;
case 3: printf("\nEnter the element to delete: ");
scanf("%d", &data);
root=del(root, data);
break;
case 4: printf("\nInorder Traversal: \n");
inorder(root);
break;
case 5: printf("\nPreorder Traversal: \n");
preorder(root);
break;
case 6: printf("\nPostorder Traversal: \n");
postorder(root);
break;
case 7: exit(0);
default:printf("\nWrong option");
break;
}
}
}
11. Develop a Program in C for the following operations on Graph(G) of Cities
a. Create a Graph of N cities using Adjacency Matrix.
b. Print all the nodes reachable from a given starting node in a digraph using DFS/BFS
method
#include <stdio.h>
#include <stdlib.h>
int a[20][20],q[20],visited[20],reach[10],n,i,j,f=0,r=-1,count=0;
void bfs(int v)
{
for(i=1;i<=n;i++)
if(a[v][i] && !visited[i])
q[++r]=i;
if(f<=r)
{
visited[q[f]]=1;
bfs(q[f++]);
}
}
void dfs(int v)
{
int i;
reach[v]=1;
for(i=1;i<=n;i++)
{
if(a[v][i] && !reach[i])
{
printf("\n %d->%d",v,i);
count++;
dfs(i);
}
}
}
void main()
{
int v, choice;
printf("\n Enter the number of vertices:");
scanf("%d",&n);
for(i=1;i<=n;i++)
{
q[i]=0;
visited[i]=0;
}
for(i=1;i<=n-1;i++)
reach[i]=0;
printf("\n Enter graph data in matrix form:\n");
for(i=1;i<=n;i++)
for(j=1;j<=n;j++)
scanf("%d",&a[i][j]);
while(1)
{
printf("\n1.BFS\n2.DFS\n3.Exit\n");
scanf("%d",&choice);
switch(choice)
{
case 1: printf("\n Enter the starting vertex: ");
scanf("%d",&v);
bfs(v);
if((v<1)||(v>n))
{
printf("\n Bfs is not possible");
}
else
{
printf("\n The nodes which are reachable from %d:\n",v);
for(i=1;i<=n;i++)
if(visited[i])
printf("%d\t",i);
}
break;
case 2:dfs(1);
if(count==n-1)
printf("\n Graph is connected");
else
printf("\n Graph is not connected");
break;
case 3: exit(0);
}
}
}
12. Given a File of N employee records with a set K of Keys (4-digit) which uniquely determine
the records in file F. Assume that file F is maintained in memory by a Hash Table (HT) of m
memory locations with L as the set of memory addresses (2-digit) of locations in HT. Let the
keys in K and addresses in L are Integers. Develop a Program in C that uses Hash function H:
K →L as H(K)=K mod m (remainder method), and implement hashing
technique to map a given key K to the address space L. Resolve the collision (if any) using
linear probing.
#include <stdlib.h>
#define MAX 100
int create(int);
void linear_prob(int[], int, int);
void display (int[]);
void main()
{
int a[MAX],num,key,i;
int ans=1;
printf(" collision handling by linear probing : \n");
for (i=0;i<MAX;i++)
{
a[i] = -1;
}
do
{
printf("\n Enter the data");
scanf("%4d", &num);
key=create(num);
linear_prob(a,key,num);
printf("\n Do you wish to continue ? (1/0) ");
scanf("%d",&ans);
}while(ans);
display(a);
}
int create(int num)
{
int key;
key=num%100;
return key;
}
void linear_prob(int a[MAX], int key, int num)
{
int flag, i, count=0;
flag=0;
if(a[key]== -1)
{
a[key] = num;
}
else
{
printf("\nCollision Detected...!!!\n");
i=0;
while(i<MAX)
{
if (a[i]!=-1)
count++;
i++;
}
printf("Collision avoided successfully using LINEAR PROBING\n");
if(count == MAX)
{
printf("\n Hash table is full");
display(a);
exit(1);
}
for(i=key+1; i<MAX; i++)
if(a[i] == -1)
{
a[i] = num;
flag =1;
break;
}
//for(i=0;i<key;i++)
i=0;
while((i<key) && (flag==0))
{
if(a[i] == -1)
{
a[i] = num;
flag=1;
break;
}
i++;
}
}
}
void display(int a[MAX])
{
int i,choice;
printf("1.Display ALL\n 2.Filtered Display\n");
scanf("%d",&choice);
if(choice==1)
{
printf("\n the hash table is\n");
for(i=0; i<MAX; i++)
printf("\n %d %d ", i, a[i]);
}
else
{
printf("\n the hash table is\n");
for(i=0; i<MAX; i++)
if(a[i]!=-1)
{
printf("\n %d %d ", i, a[i]);
continue;
}
}
}
