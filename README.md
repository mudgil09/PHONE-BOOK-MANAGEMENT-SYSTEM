#include<stdio.h>
#include<stdlib.h>
#include<string.h>
typedef struct list add;
add *start;
struct list
{
	struct entry *lptr;
	char name[50];
	char num[11];
	add* next;
};
int i=1;
char t; //global variable
void Insert();
void Delete();
void delete_same_name();
void search();
void display();
int no_of_nodes();
void sort();

void sort()
{
    struct list *temp,*pretemp,*p,*r,*s,*t;
    int n;
    n=no_of_nodes();
    for(int i=n;i!=0;i=i-1)
    {
        temp=start;
        t=start;
        pretemp=start->next;
        while(pretemp!=NULL)
        {
            if(strcmp(temp->name,pretemp->name)>0)
            {
                p=temp;
                r=pretemp;
                if(temp==start)
                {
                    p->next=r->next;
                    r->next=p;
                    temp=r;
                    pretemp=p;
                    start=temp;
                }
                else{
                    s=t;
                    s->next=r;
                    p->next=r->next;
                    r->next=p;
                    temp=r;
                    pretemp=p;
                }
            }
            t=temp;
            temp=temp->next;
            pretemp=pretemp->next;
        }
    }
}

int no_of_nodes()
{
    struct list *temp;
    temp=start;
    int i=0;
    while(temp!=NULL)
    {
        temp=temp->next;
        i++;
    }
    return i;
}
void Insert()
{
	add *temp=(add*)malloc(sizeof(add));
	printf("\nContact name : ");
	scanf("%c",&t);
	gets(temp->name);
	printf("\nMobile Number : ");
	gets(temp->num);
	temp->next = NULL;

	if(start == NULL)
	{
		start = temp;
		printf("\nRecord added");
		return; //come out of whole fn insert
	}
	else
	{
		add* p = start;
		while(p->next != NULL)
			p = p->next;
		p->next = temp;
		printf("\nRecord added");
	}
}

void Delete()
{
	char ch[40];
	printf("\nContact name : ");
	scanf("%c",&t);
	gets(ch);

	if(start == NULL)
		printf("\nNo contact exists in the Phonebook");
	else
	{
		if(strcmp((start->name),ch)==0)
		{
			add *p = start;
			start = start->next;
			free(p);
			printf("\nRecord deleted");
		}
		else
		{
			add*p = start;
			while(p->next != NULL)
			{
				if(strcmp((p->next->name),ch)==0)
				{
					p->next = p->next->next;
					return;
				}
				p = p->next;
			}
			printf("\nInvaild Contact");
		}
	}
}
void delete_same_name() //0-false
{
	add*p = start;
	char ch[50],str[50];
	printf("\nContact name : ");
	scanf("%c",&t);
	gets(ch);
	if(strcmp((start->name),ch)!=0) // delete if it is not start node
	{
			while(p->next != NULL)
			{
				if(strcmp((p->next->name),ch)==0)
				{
					p->next = p->next->next;
					printf("\nRecord deleted");
					return;
				}
				p = p->next;
			}
			printf("\nInvaild Contact");
			}
else
	{
			start = start->next;
			free(p);
			printf("\nRecord deleted");
	}
}
void search()
{
	char ch[40];
	printf("\nContact name : ");
	scanf("%c",&t);
	gets(ch);

	if(start == NULL)
	 printf("\nNo records are in phonebook");
	else
	{
	add *p = start;
	while(p!=NULL)
	{
		if(strcmp((p->name),ch)==0)
		{
			printf("\n%s",p->name);
			printf("\n%s",p->num);
			return;
		}
		p = p->next;
	}
	printf("\nContact is not exist in the list");
	}
}

void display()
{
    sort();
	if(start == NULL)
		printf("\nNo contacts exists in the phonebook");
	else
	{
		add*p = start;
		while(p != NULL)
		{
			printf("\n%d. %s",i,p->name);
			printf("\nNumber : %s",p->num);
			p = p->next;
			i++;
		}
		i=1;
		return;
	}
}

int main()
{
	add* start = NULL;
	char c[40];
	int choice;

	while(choice != 6)
	{
	printf("\n****************--------MINI PROJECT-PHONEBOOK MANAGEMENT SYSTEM--------****************");
printf("\n1.Enter the new contact\n2.Delete the contact by name\n3.Delete the contact having same name\n4.Search the contact\n5.Display all the contacts\n6.Exit");
		printf("\nEnter your choice : ");
		scanf("%d",&choice);
		switch(choice)
		{
			case 1: Insert();
					break;
			case 2: Delete();
					break;
			case 3: delete_same_name();
					break;
			case 4: search();
					break;
			case 5: display();
					break;
			case 6: exit(0);
			default : printf("Invalid choice");
		}
	}
}

