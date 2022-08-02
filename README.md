#include<conio.h>
#include<stdlib.h>
#include<string.h>
#include<windows.h>
void adminpa#include<stdio.h>
ge();
void addrecord();
void modifyrecord();
void deleterecord();
void bookticket();
void page1();
void record();
int info(int);
struct passenger{
int num,age;
char name[20],address[20], phone[10]
}j;
int main()
{
int a,c,d,y;
char username[100]="JKH";
char b[100];
printf("\tWelcome to JKH Airlines Ticket Reservation System\n\tBooking your flight tickets at lowest airfare");
invalid:
    printf("\n\n\t\t\t1.Admin page\n");
    printf("\t\t\t2.Ticket Reservation\n");
    printf("\t\t\t3.Exit.\n\n");
    printf("\n\t\t\tChoose a number:");
    scanf("%d",&a);
switch(a)
{
case 1:
system("cls");
printf("Enter your username:\n");
scanf("%s",b);
printf("Enter your password:\n");
scanf("%d",&c);
y=(strcmp(b,username)==0)&&(c==616768);
if(y==1)
{
printf("Password matched\nPlease wait a few seconds.");
Sleep(1000);
adminpage();
}
else
printf("You have entered wrong username or password! ");
break;

case 2:
system("cls");
bookticket();
break;

case 3:
exit(0);
}
    if (a!=1&&a!=2&&a!=3)
       {
           system("cls");
           printf("You have entered wrong number.\nPlease enter 1,2 or 3.\n ");
           goto invalid;

       }
return 0;
}
void adminpage()
{
int e;
printf("\t\t\t\nYou are welcome\n");
printf("1.Add Record.\n");
printf("2.Modify Record\n");
printf("3.Delete Record\n");
printf("4.Back\n");
printf("\n\nChoose a number :");
scanf("%d",&e);
switch (e)
{
case 1:
    system("cls");
    addrecord();
    break;
case 2:
    system("cls");
    modifyrecord();
    break;
case 3:
    system("cls");
    deleterecord();
    break;
case 4:
    system("cls");
    main();
    break;
}

    if (e!=1 && e!=2 && e!=3 && e!=4)

       {
           system("cls");
           printf("You have entered wrong number.\nPlease choose 1,2, 3 or 4.\n\n\n ");
           adminpage() ;
        }
}
void addrecord()
{
    FILE *afp;
    afp=fopen("addrecord.txt","rb");
    int seats,f,seatno[15];
     printf("\t\tJKH AIRLINES\n");
        printf("_________________________________________________________\n");
        printf("Seats:\n");
        printf("\n\n1  12\n\n\n\t\t\t 21  22  23\n\n\n\t\t\t 31  32\n\n41\t\t\t 42  43  44\n\n\n51\t52\t53\t54\t55");
        printf("\n\n\nNo. of seats :  ");
        scanf("%d",&seats);
        printf("Which %d seats do you want to reserve?: \n",seats);
        for (f=0;f<seats;f++)
        {
                mec:
                printf("Seat%d    :",f+1);
                scanf("%d",&seatno[f]);
        }
                while (fread(&j,sizeof(j),1,afp)==1)

        {

                for(f=0;f<seats;f++)
               {

                  if (seatno[f]==j.num)
                    {
                       printf("Seat%d already reserved.Try next.\n",seatno[f]);
                       goto mec;
                    }
                }
        }
        fclose(afp);

        info(seats);


}
void modifyrecord()
{
  char name1[30];
  int data_found=0;
  int recordno=0;
  FILE *afp;
  afp=fopen("addrecord.txt","rb+");
  if (afp==NULL)
  {
      printf("Error opening file..");
      exit(1);
  }
  printf("Enter the name of the passenger whose record is to be modified:");
  scanf("%s",&name1);
  fflush(stdin);
  while(fread(&j,sizeof(j),1,afp)==1)
  {
      if(strcmp(j.name,name1)==0)
      {
          data_found++;
          printf("The old record is:");
          printf("Name\tDestination\tAge\tContactno.\tseatno.\n");
            printf("---------------------------------------------------------------------------\n");
            printf("\t\t%s\t%s\t%d\t%s\t%d\n",j.name,j.address,j.age,j.phone,j.num);
            printf("\nPlease enter new data below.\n");
                        printf("Name:");
            scanf("%s",j.name);
            printf("Destination:");
            scanf("%s",j.address);
            printf("Age:");
            scanf("%d",&j.age);
            printf("Phone no:");
            scanf("%s",j.phone);
            printf("Seat no.:");
            scanf("%d",&j.num);
            fseek(afp,sizeof(j)*recordno,SEEK_SET);
            fwrite(&j,sizeof(j),1,afp);
            printf("The record has been modified!!\n");
            break;
      }
      recordno++;
      if (data_found==0)
        {
            printf("No such record found...\n Please re-enter the name.");
            modifyrecord() ;
                 }

    fclose(afp);
    getch();
    }
  }
  void deleterecord()
  {
     char g[20];
     char c;
     int h;
     FILE*afp,*bfp;
     afp=fopen("addrecord.txt","rb");
     if (afp==0)
     {
         printf("File not found");
         exit(1);

     }
     bfp=fopen("temporary.txt","wb");
     if (bfp==0)
     {
         printf("File not found");
         exit(1);
     }
         printf("Enter the name of passenger to be deleted :");
    scanf("%s",g);
    while (fread(&j,sizeof(j),1,afp)==1)
    {
        if (strcmp(j.name,g)!=0)
        {
            fwrite(&j,sizeof(j),1,bfp);
        }
    }
    remove("addrecord.txt");
    rename("temporary.txt","addrecord.txt");
    fclose(afp);
    fclose(bfp);
    printf("\nThe record was successfully deleted\n");
     printf("Press Enter to complete or any other key to exit.");
    c=getch();
    if (c=='\n')
    {
        system("cls");
        adminpage();

  }
  }
  void bookticket()
  {
    int h,k;
    char c;
    printf("\n\t\t\Welcome to the flight reservation system.\n\n\n");
        printf("\n\t\t\t1.Reserve Seats.\n");
        printf("\t\t\t2.Reserved seats info.\n");
        printf("\t\t\t3.Passengers info.\n");
        printf("\t\t\t4.Back.");
        printf("\nChoose a number as per your need : ");
        scanf("%d",&h);
            switch (h)
    {
    case 1:
        system("cls");
       addrecord();
        break;
    case 2:
        system("cls");
       printf("\t\t\tHere are the information of all the\n \t\t\treserved seats and individual name\n\n\n");
       record();
        printf("Press Enter to complete or any other key to exit.");
    k=getch();
    if (k=='\n')
    {
        system("cls");
        record();
    }
    else
    exit(0);
       break;
    case 3:
        system("cls");
        page1();
         printf("\nPress Enter to complete or any other key to exit.");
    c=getch();
    if (c=='\n')
    {
        system("cls");
        bookticket();

    }
    else
    exit(0);

    break;
    case 4:
        system("cls");
        main();
        break;
    }
}
void page1()
{
    FILE *afp;
    afp=fopen("addrecord.txt","rb");
    if (afp==NULL)
    {
        printf("File is unable to open");
        exit(0);
    }
    while (fread(&j,sizeof(j),1,afp)==1)
    {
        printf("Name:%s\nDestination:%s\nAge:%d\nPhone no. :%s\n\n\n",j.name,j.address,j.age,j.phone);
    }
    fclose(afp);
}
void record()
{
    FILE *afp;
    afp=fopen("addrecord.txt","rb");
    if (afp==NULL)
    {
        printf("File is unable to open");
        exit(0);
    }
    while (fread(&j,sizeof(j),1,afp)==1)
    {
        printf("Seat  %d\t%s\t    %s\t%s\n",j.num,j.name,j.address,j.phone);
    }
    fclose(afp);
}
int info(int seats)
{
    FILE *afp;
    struct passenger j;
     int l;
     char n;
    afp=fopen("addrecord.txt","ab");
    for(l=0;l<seats;l++)
    {
        printf("\nConfirm your seat no%d    :",l+1);
        scanf("%d",&j.num);
        printf("\nName: ");
        scanf("%s",j.name);
        printf("\nDestination: ");
        scanf("%s",j.address);
        printf("\nAge: ");
        scanf("%d",&j.age);
        printf("\nPhone no. : ");
        scanf("%s",j.phone);
        printf("\n\n");
        fwrite(&j,sizeof(j),1,afp);

    }
    fclose(afp);
    printf("You have succesfully reserved your seat!!");
    printf("Press Enter to complete or any other key to exit.");
    n=getch();
    if (n=='\n')
    {
      system("cls");
      bookticket;

    }
    else
    exit(0);
    return 0;
    }
