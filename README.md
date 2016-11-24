//operates for linklist ...there are some error ...
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
struct Node{
	long num;
	float grade;
	struct Node *next;
};
struct Node *Creatlinklist(){
	int k;
	long nn;
	struct Node *headp,*newp,*tailp;
	headp=NULL;
	k=0;
	printf("please input a student number:");
	scanf("%ld",&nn);
	while(nn!=0l){
	    k++; 
		newp=(struct Node *)malloc(sizeof(struct Node *));
		newp->num=nn;
		printf("please input grade:");
		scanf("%f",&newp->grade);
		if(k==1)
			headp=newp;
		else
	     	tailp->next=newp;
		tailp=newp;
		printf("please input next student number:");
		scanf("%ld",&nn);
	}

	tailp->next=NULL;
	free(newp);
	return(headp);
} 
void Outputlinklist(struct Node *headp){
	struct Node *p;
	if(headp==NULL){
		printf("empty list,no data here!");
		return;
	}
	p=headp;
    while(p!=NULL){
    	printf("num:%ld grade:%.2f \n",p->num,p->grade);
    	p=p->next;
	}	
}
struct Node *Deletelinklist(struct Node *headp,long number){
	struct Node *cheak,*last,*p;
	cheak=last=headp;
	while(cheak!=NULL){
		if(cheak->num==number)
			break;
		last=cheak;
		cheak=cheak->next;
	}
	if(cheak->num==number){
		if(cheak==headp){
			headp=cheak->next;
		}
		else
		last->next=cheak->next;
		free(cheak);
		printf("student %ld is deleted!\n",number);
		
	}
	else
	printf("there is no student %ld",number);
	return(headp);
} 
struct Node *Sortlinklist(struct Node *headp){//按学号排序 
	struct Node *p,*last,*cheak,*t;
	int n,i,j;
	p=headp;
	cheak=headp->next;
	if(headp==NULL){
		printf("empty linklist!");
		return(headp);
	}
	for(n=0;p!=NULL;n++){
    	p=p->next;
	}	
	printf("%d\n",n);
	for(i=0;i<n-1;i++){
  
	for(j=0;j<n-1;j++) 
	{
		if(last->num>cheak->num){
	    t=last;	
		last=cheak;	
		cheak=t;
		cheak=cheak->next;
    	}
		last=last->next;
	    }
    }
	return(headp);	
}
struct Node *Insertlinklist(struct Node *headp,struct Node *insert ){
/*	struct Node *cheak,*last,*tailp;
	cheak=last=headp;
	if(cheak==NULL){//empty list,establish a new linklist
	headp=insert;
	insert->next=NULL;
	return(headp);
	}
    while(cheak!=NULL){
    	//find the insert node
    	if(insert->num<headp->num){
    		insert->next=headp;
    		return(insert);
		}
    	if(last->num<=insert->num&&cheak->num>=insert->num)
			break;
		last=cheak;
		cheak=cheak->next;
	}
	//insert
	insert->next=cheak; 
	last->next=insert;
	return(headp);
	*/
	struct Node *last,*cheak,*p;
	p=last=cheak=headp;
	if(headp==NULL){
		insert->next=NULL;
		return(insert);
	}
	else if(insert->num<headp->num){
		insert->next=headp;
		return(insert);
	}
	while(cheak!=NULL){
		if(cheak->num>insert->num&&last->num<insert->num)	
		break;
		last=cheak;
		cheak=cheak->next;
	} 
	if(cheak->num>insert->num&&last->num<insert->num){
		last->next=insert;
		insert->next=cheak;
		return(headp);
	}

	else if(last->num<insert->num){
		last->next=insert;
		insert->next=NULL;
		return(headp);
	}	 
}
main(){
struct Node *headp,*insert;
long number;
insert=(Node *)malloc(sizeof(Node *));
insert->num=6l;
insert->grade=60;
printf("please input the record:\n");
headp=Creatlinklist();
Outputlinklist(headp);
printf("please input the number you want to delete:");
scanf("%ld",&number);
printf("\n\n");
Outputlinklist(Deletelinklist(headp,number));
printf("\n\n");
Outputlinklist(Sortlinklist(Deletelinklist(headp,number)));
printf("\n\n");
Outputlinklist(Insertlinklist(Sortlinklist(Deletelinklist(headp,number)),insert));
free(headp);
free(insert); 
getch();	
}
