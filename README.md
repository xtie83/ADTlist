/*Write the Student Record Program using Parallel Arrays implementation of
ADT List Operations with records sorted by names and no duplicate names allowed.

Menu
1. Add Record
2. Delete Record
3. Display All
4. Exit */

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX 5

typedef struct studentrecords{
    char name[MAX][30];
    int q1[MAX];
    int q2[MAX];
    int q3[MAX];
    int last;

} LIST;

LIST L;
void makenull();
void add(char n[30], int q1, int q2, int q3);
void del (char n[30]);
void display();
int locate(char n[30]);
int isFull();
int isEmpty();
int menu();
float avg(int q1, int q2, int q3);
int searchPos(char n[30]);

int main(){
char nm[31];
int q1, q2, q3;
int stud_in_list;
int do_exist;
makenull();

while(1){

    switch(menu()){
    case 1: system("cls");printf("Student Record\n");
            printf("Enter Student Name : ");scanf(" %[^\n]%*c",nm);
            stud_in_list = locate(nm);
            do_exist = strcmp(nm,L.name[stud_in_list]);
                if (do_exist == 0) {
                    printf("Student Name Already Exist!\n");
                    system("pause");
                    }
                else {
                printf("Input Quiz 1: ");scanf("%d",&q1);
                printf("Input Quiz 2: ");scanf("%d",&q2);
                printf("Input Quiz 3: ");scanf("%d",&q3);
                add(nm,q1,q2,q3);
                }
                break;

    case 2: system("cls");printf("Delete Mode\n");
            printf("Enter student name: ");scanf("%s",nm);
            del(nm);break;

    case 3: display();break;

    case 4: exit(0);

    default: printf("\nInvalid input. Select 1 to 4 only.\n");system("pause");
        }
    }
}

void makenull(){
    L.last = -1;
}

void add(char n[30], int q1, int q2, int q3){
    int i,p;
    if (isFull()){
            printf("List is full.\n");
            system("pause");
            }
    else{
         p=searchPos(n);
         for (i=L.last;i>=p;i--){
            strcpy(L.name[i+1],L.name[i]);
            L.q1[i+1]=L.q1[i];
            L.q2[i+1]=L.q2[i];
            L.q3[i+1]=L.q3[i];
         }
        strcpy(L.name[p],n);
        L.q1[p]=q1;
        L.q2[p]=q2;
        L.q3[p]=q3;
        L.last++;
         }
}

void del(char n[30]){
    int p,i;
    if (isEmpty()){
        printf("List is empty.\n");
        system("pause");
    }
    else{
        p=locate(n);
        if (p<0){
            printf("Not found.\n");
            system("pause");

            }
        else{
            for (i=p;i<=L.last;i++){
            strcpy(L.name[i],L.name[i+1]);
            L.q1[i]=L.q1[i+1];
            L.q2[i]=L.q2[i+1];
            L.q3[i]=L.q3[i+1];
            }
            L.last--;
        }
    }
}
void display(){
int i;
float ave;
system("cls");
        printf("Student Name    Quiz 1   Quiz 2    Quiz 3   Average     Remarks\n");

        for(i=0;i<=L.last;i++){
        ave=avg(L.q1[i],L.q2[i],L.q3[i]);

        printf("%d.) %s\t%d\t%d\t%d\t%4.2f\t%s\n",i+1,L.name[i],L.q1[i],L.q2[i],L.q3[i],ave,ave>=75? "Passed":"Failed");
        }
        system("pause");
}

int locate(char n[31]){
int i;
    for (i=0;i<=L.last;i++){
        if (strcmp(L.name[i], n)==0)
                return (i);
    }
    return (-1);
}

int isFull(){
    return (L.last==MAX-1);
}
int isEmpty(){
    return (L.last==-1);
}

int menu(){
int op;
system("cls");
    printf("Menu\n");
    printf("1. Add Record\n");
    printf("2. Delete Record\n");
    printf("3. Display All\n");
    printf("4. Exit\n");
    printf("\nSelect 1-4: ");
    scanf("%d",&op);
return(op);
}

float avg(int q1, int q2, int q3){
return (q1+q2+q3)/3.0;
}
int searchPos(char n[31]){
int i;
for (i=0;i<=L.last;i++){
    if ((strcmp(L.name[i],n)>=0))
        return i;
    }
return i;
}




















