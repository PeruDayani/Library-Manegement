#include<conio.h>
#include<fstream.h>
#include<string.h>
#include<stdio.h>
#include<dos.h>

char* convert(int code);
void choosebook();
void mainmenu();
void login();
int check(char name[50]);
void newuser();
void usermenu(char username[50]);
void issuebook(char username[50]);
int checkcode(int code);
void displaybooks();
void displayauthors();
void displaytypes();
void returnbook(char username[50]);
void changepass(char username[50]);
void deleteacc(char username[50]);
void showissued(char username[50]);
void admincheck();
void adminmenu();
void newbook();
void removebook();
void viewuserlist();
void viewuserinfo();
void viewbooklist(char back[80]);
void resetlib();
void editrecord();
void initialize();


void main()
{
 textbackground(WHITE);
 textcolor(BLUE);

 clrscr();

 mainmenu();

 getch();
}


class Booklist
{
 private:

	 char bookname[70];
	 char booktype[70];
	 char bookauthor[70];
	 int bookcode;

 public:
	 Booklist()
		{
		 strcpy(bookname,"No book issued.");
		 strcpy(booktype,"No book issued.");
		 strcpy(bookauthor,"No book issued.");
		 bookcode=100;
		}

	 Booklist(char name[70],char author[70],char type[50],int code)
		{
		 strcpy(bookname,name);
		 strcpy(bookauthor,author);
		 strcpy(booktype,type);
		 bookcode=code;
		}

	 void addbook()
		{
			cout<<"Enter the author of the book: ";
			gets(bookauthor);
			cout<<"Enter the name of the book: ";
			gets(bookname);
			cout<<"Enter the type of the book: ";
			gets(booktype);
			cout<<"Enter the book code       : ";
			cin>>bookcode;
		}

	 void displaybook()
		{
		 if(bookcode!=100)
			{
			 cout<<"The name of the book  : ";
			 cout<<bookname<<endl;
			 cout<<"The author of the book: ";
			 cout<<bookauthor<<endl;
			 cout<<"The type of the book  : ";
			 cout<<booktype<<endl;
			 cout<<"The book code         : ";
			 cout<<bookcode<<endl;
			}
		}

	 void displaybooks()
		{
		 cout<<bookcode<<" : "<<bookname<<" by "<<bookauthor<<endl;
		}

	 void removebook()
		{
			 strcpy(bookname,"No book issued.");
			 strcpy(booktype,"No book issued.");
			 strcpy(bookauthor,"No book issued.");
			 bookcode=100;
		}

	 char* Rbookname()
		{
		 return (bookname);
		}

	 int Rbookcode()
		{
		 return (bookcode);
		}

	 char* Rbookauthor()
		{
		 return (bookauthor);
		}

	 char* Rbooktype()
		{
		 return (booktype);
		}

	 void Editbookname()
		{
		 cout<<"Enter the correct book name: ";
		 gets(bookname);
		}

	 void Editbookauthor()
		{
		 cout<<"Enter the correct book author: ";
		 gets(bookauthor);
		}

	 void Editbooktype()
		{
		 cout<<"Enter the correct book type: ";
		 gets(booktype);
		}
};

class User
{
 private:
	 char username[50];
	 char password[50];
	 int bissued[5];
	 int noissued;
 public:
	 User()
		{
		 bissued[0]=100;
		 bissued[1]=100;
		 bissued[2]=100;
		 bissued[3]=100;
		 bissued[4]=100;
		 noissued=0;
		}

	 void adduser(char name[80]);

	 char* Rusername()
		{
		 return (username);
		}
	 char* Rpassword()
		{
		 return (password);
		}
	 int Rnoissued()
		{
		 return noissued;
		}

	 void bissue(int fcode);

	 void breturn(int rcode);

	 void dispissued();

	 void inputnewpass();

	 void userinfo()
		{
		 cout<<"USERNAME: ";puts(username);
		 cout<<"PASSWORD: ";puts(password);
		 dispissued();
		}
};

void User::dispissued()
{
	int count=0;

	cout<<"The books issued by the user are:"<<endl;

	for(int i=0;i<5;i++)
	 if(bissued[i]==100)
		count++;


	if(count==5)
	 {
		cout<<" No books issued yet."<<endl;
	 }
	else
	 {
		for(int k=0;k<5;k++)
		 {
			if(bissued[k]!=100)
			 {
				cout<<bissued[k]<<":";
				puts(convert(bissued[k]));
			 }
		 }
	 }

}

void User::bissue(int fcode)
{
	int found=0;
	for(int i=0;i<5;i++)
	 if(found==0 && bissued[i]==100)
		 {
	found++;
	bissued[i]=fcode;
		 }
	noissued++;
}


void User::adduser(char name[80])
{
	clrscr();

	strcpy(username,name);

	cout<<"Welcome ";
	puts(username);


	cout<<"Please enter your password:"<<endl;

	int i=0;
	char in;
	do
	 {
		in=getch();
		if(in!=(char)13)
		 {
			 cout<<"*";
			 password[i++]=in;
		 }
	 }while(in!=(char)13);
	password[i]='\0';

}

void User::breturn(int rcode)
{
 if(rcode!=100)
	 {
		int found=0;
		for(int i=0;i<5;i++)
		 if(bissued[i]==rcode && found==0)
			{
			 found++;
			 bissued[i]=100;
			}

		if (found==1)
		 {
			noissued--;
			cout<<"The book has been returned."<<endl;
			cout<<"Thank you and do visit again."<<endl;
		 }
		else
		 {
			cout<<"You have entered an invalid code."<<endl;
		 }

	 }
	else
	 {
		cout<<"No book has been returned"<<endl;
	 }
}

void User::inputnewpass()
{
 clrscr();
 char check[50];

 cout<<"Please enter your new password:"<<endl;
 gets(password);

 do
 {
	cout<<"Confirm password:"<<endl;
	gets(check);
 }while( strcmp(password,check)!=0);


 cout<<"Password succcessfully changed."<<endl;
 cout<<"Press enter to return to the user menu.";
 getch();
}


char* convert(int code)
{
 fstream fil;
 fil.open("booklist.dat",ios::in|ios::binary);

 Booklist B;
 int found=0;
 char bookname[70];

 while( fil.read((char*)&B,sizeof(B)) && !found)
	 {
		if( code==B.Rbookcode() )
		 {
			found++;
			strcpy(bookname,B.Rbookname());
		 }
	 }

 fil.close();

 if(code==100)
	strcpy(bookname,"No Book Issued.");

 return (bookname);

}

void mainmenu()
{
	char choice;

	clrscr();
	cout<<"   MAIN MENU:"<<endl<<endl;
	cout<<"     A.Login"<<endl;
	cout<<"     B.New User"<<endl;
	cout<<"     C.Admin"<<endl;
	cout<<"     D.Quit"<<endl<<endl;
	cout<<"   Choose a option: ";
	cin>>choice;
	cout<<endl;

	switch (choice)
	 {
		case 'A':
		case 'a': login();
			  break;

		case 'B':
		case 'b': newuser();
			  break;

		case 'C':
		case 'c': admincheck();
			  break;

		case 'D':
		case 'd': cout<<"Thank you for coming."<<endl;
			  cout<<"Press enter to exit.";
			  break;

		default : clrscr();
			  cout<<"You entered an invalid option."<<endl;
			  mainmenu();
	 }
}

void login()
{

 char  name[50],pass[50];
 User A;
 int found=0;
 int count=0;
 int i=0;

 cout<<"Welcome back!!!"<<endl;
 cout<<"Enter your username: ";gets(name);

 fstream fil;
 fil.open("library.dat",ios::in|ios::binary);

 while( fil.read((char*)&A,sizeof(A)) && !found)
   {
      if( strcmp( name,A.Rusername() )==0 )
       {
	found++;

	while(strcmp(pass,A.Rpassword())!=0 && count<3)
	   {
	    cout<<3-count<<" chances left."<<endl;
	    count++;

	    cout<<"Enter your password: ";

	    i=0;
	    char in;
	    do
	    {
	     in=getch();
	     if(in!=(char)13)
	      {
	       cout<<"*";
	       pass[i++]=in;
	      }
	    }while(in!=(char)13);
	    pass[i]='\0';
	    cout<<endl;

	   } // while loop termination for checking password


	if(count==3)
	 {
	  cout<<"Wrong user? press enter to go back to main menu.";
	  getch();
	  fil.close();
	  mainmenu();
	 }
	else
	 {
	  fil.close();
	  usermenu(A.Rusername());
	 }

       } //if loop termination when we found user

   } //while loop termination when we read reords

  if(found==0)
   {
    cout<<"Username does not exist..."<<endl;
    cout<<"Press enter to go back to main menu.";
    fil.close();
    getch();
    mainmenu();
   }

} //function termination

int check(char name[80])
{

 int found=0;

 fstream fil;
 fil.open("library.dat",ios::in|ios::binary);

 User A;

 while( fil.read( (char*)&A,sizeof(A) ) )
     if(strcmpi(A.Rusername(),name)==0)
      found++;

 return(found);

}

void newuser()
{
    char name[80];

    fstream fil;
    fil.open("library.dat",ios::app|ios::binary);

    User B;

    cout<<"Enter a username: ";
    gets(name);

    if(check(name)!=0)
     {
      cout<<"This username is already taken."<<endl;
      fil.close();
      newuser();
     }
    else
     {
      B.adduser(name);

      fil.write( (char*)&B,sizeof(B) );
      fil.close();

      cout<<endl;
      cout<<"Thank you for signing up!!"<<endl;
      cout<<"Press enter to proceed to user menu."<<endl;
      getch();

      usermenu(name);
     }

}

void usermenu(char username[50])
{
 clrscr();

 User A;
 fstream fil;
 fil.open("library.dat",ios::in|ios::binary);

 int found=0;
 while( fil.read((char*)&A,sizeof(A)) && !found)
	{
		if(strcmp(username,A.Rusername())==0)
		 {
			 found++;

			 char choice;

			 clrscr();
			 cout<<"Welcome ";puts(username);
			 cout<<"USER MENU:"<<endl<<endl;
			 cout<<"A.Issue new book"<<endl;
			 cout<<"B.Return issued book"<<endl;
			 cout<<"C.Change password"<<endl;
			 cout<<"D.Delete account"<<endl;
			 cout<<"E.Show books issued"<<endl;
			 cout<<"F.Sign out"<<endl;
			 cout<<"choose a option: ";
			 cin>>choice;

			 switch (choice)
	 {
		case 'A':
		case 'a':   fil.close();
			 issuebook(username);
			 break;

		case 'B':
		case 'b':   fil.close();
			 returnbook(username);
			 break;

		case 'C':
		case 'c':   fil.close();
			 changepass(username);
			 break;

		case 'D':
		case 'd':   fil.close();
			 deleteacc(username);
			 break;

		case 'E':
		case 'e':   fil.close();
			 showissued(username);
			 break;

		case 'F':
		case 'f':clrscr();
			 cout<<"Press enter to sign out."<<endl;
			 fil.close();
			 getch();
			 mainmenu();
			 break;

		default :cout<<"Choice invalid, press enter to return to the usermenu.";
			 fil.close();
			 getch();
			 usermenu(username);
	 }
		 }
	}

 }


void issuebook(char username[50])
{
 clrscr();

 int fcode;

 User A;
 fstream fil;
 fil.open("library.dat",ios::in|ios::out|ios::binary);

 int found=0;

 while( fil.read((char*)&A,sizeof(A)) && !found)
  if(strcmp(username,A.Rusername())==0)
   {
    found++;

    if(A.Rnoissued()<5)
     {
      choosebook();

      cout<<endl;
      cout<<"If you do not wish to issue a book input 100 "<<endl;
      cout<<"If there are no books available enter 100."<<endl;
      cout<<"Enter the code of the book you want: ";
      cin>>fcode;

       if( checkcode(fcode)==1 || fcode==100)  //validcodecheck
	{
	 if(fcode!=100)   //100,issue or not
	  {
	    char ch;

	    cout<<endl;
	    cout<<"Are you sure you wish to issue this book ? "<<endl;
	    cout<<"* ";puts( convert(fcode) );
	    cout<<"(y/n) :";
	    cin>>ch;

	    if(ch=='y' || ch=='Y')
	     {
	      A.bissue(fcode);
	      int pos=( fil.tellg()-sizeof(A) );
	      fil.seekg(pos);
	      fil.write( (char*)&A,sizeof(A) );

	      cout<<endl;
	      cout<<"The book has been issued by you."<<endl;
	      cout<<"Press enter to proceed to the user menu.";
	      getch();

	      fil.close();

	      usermenu(username);
	     }
	    else
	     {
	       cout<<endl;
	       cout<<"No book has been issued."<<endl;
	       cout<<"Press enter to return to the user menu."<<endl;
	       getch();

	       fil.close();

	       usermenu(username);
	     }

	  }
	 else   //not book to be issued if 100 entered
	  {
	   cout<<endl;
	   cout<<"No book has been issued."<<endl;
	   cout<<"Press enter to proceed to the user menu.";
	   getch();
	   fil.close();

	   usermenu(username);
	  }
	} //termiantion of if valid code
       else    // else for invalid code
	{
	 cout<<endl;
	 cout<<"You have entered an invalid code."<<endl;
	 cout<<"Press enter to return to the user menu."<<endl;
	 getch();
	 fil.close();

	 usermenu(username);
	}  //termination for else for invalid code

     }  //termination for check if book can be issued
    else  // else for if 5 books are already issued.
     {
      cout<<endl;
      cout<<"You corrently have 5 books issued."<<endl;
      cout<<"Please return at least one book to issue a new one."<<endl;
      cout<<"Press enter to return to the usermenu.";
      fil.close();
      getch();

      usermenu(username);
     }    // termination for else for more than 5 books issued

   } //termination of the while/if loop

} // functionf termination

void choosebook()
{
 char ch, search[50];

 clrscr();

 cout<<"Hello! how do you wish to search for a book: "<<endl;

 cout<<"A.View all."<<endl;
 cout<<"B.By Author Name."<<endl;
 cout<<"C.By Genre."<<endl;

 cin>>ch;

 clrscr();

 switch(ch)
  {
   case 'A':
   case	'a': displaybooks();
	     break;

   case 'B':
   case	'b': displayauthors();
	     cout<<"Enter the Author name: ";
	     gets(search);
	     break;

   case 'C':
   case	'c': displaytypes();
	     cout<<"Enter the Genre: ";
	     gets(search);
	     break;

   default: cout<<"Invalid option."<<endl<<"Press enter to go back.";
	    choosebook();

  }

 fstream fil;
 fil.open("booklist.dat",ios::binary|ios::in);

 Booklist  B;
 int displayed=0;

 while( fil.read( (char*)&B,sizeof(B) ) )
  {
   switch(ch)
   {
    case 'A':
    case 'a': displayed++;
	      break;

    case 'B':
    case 'b':  if( strcmpi(B.Rbookauthor(),search)==0 )
		{
		 displayed++;
		 B.displaybooks();
		}
	       break;

    case 'C':
    case 'c':  if( strcmpi(B.Rbooktype(),search)==0 )
		{
		 displayed++;
		 B.displaybooks();
		}
	       break;

    default :  cout<<"You entered an invalid option."<<endl;
	       cout<<"Press enter to go back";
	       getch();
	       choosebook();

   }

  }

  fil.close();

  if (displayed==0)
   {
    cout<<"You entered and invalid option."<<endl;
    cout<<"Press enter to go back";
    getch();

    choosebook();
   }

}

void displaybooks()
{
 char choice='y';
 int code;

 clrscr();

 fstream fil;
 fil.open("booklist.dat", ios::in | ios::binary);
 Booklist B;

 int i=1;

 while( fil.read( (char*)&B,sizeof(B) ) && choice=='y')
  {
	if(B.Rbookcode()!=100)
	 {
	  if(i==17)
	   clrscr();

	  cout<<i<<": "<<B.Rbookcode()<<":"<< B.Rbookname() <<" by "<<B.Rbookauthor()<<endl;
	  i++;
	 }
	if(i==16)
	 {
		  cout<<"Do you wish to see more books?(y/n): ";
		  cin>>choice;
	 }
  }
 fil.close();

}

void displayauthors()
{
 char author[70];
 char authors[20][70];

 int i=1;
 int found,k;

 fstream fil;
 fil.open("booklist.dat",ios::binary|ios::in);

 Booklist  B;

 cout<<endl<<"The books avalable are: "<<endl;

 while( fil.read( (char*)&B,sizeof(B) ) )
  if(B.Rbookcode()!=100)
   {
    found=0;

    strcpy( author,B.Rbookauthor() );

    k=0;

    while(k<i && found==0 )
     {
      if( strcmpi(author,authors[k])==0  )
       found++;
      k++;
     }

    if(found==0)
     {
      strcpy(authors[i-1],author);
      i++;
     }

   }

 cout<<"Enter the type you want: "<<endl;

 for(int j=0;j<(i-1);j++)
  {
   cout<<"* "<<authors[j]<<endl;
  }

 cout<<endl;

 fil.close();
}

void displaytypes()
{

 char type[70];
 char types[20][70];

 int i=1;
 int found,k;

 fstream fil;
 fil.open("booklist.dat",ios::binary|ios::in);

 Booklist  B;

 cout<<endl<<"The books avalable are: "<<endl;

 while( fil.read( (char*)&B,sizeof(B) ) )
  if(B.Rbookcode()!=100)
   {
    found=0;

    strcpy( type,B.Rbooktype() );

    k=0;

    while(k<i && found==0 )
     {
      if( strcmpi(type,types[k])==0  )
       found++;
      k++;
     }

    if(found==0)
     {
      strcpy(types[i-1],type);
      i++;
     }

   }

 cout<<"Enter the type you want: "<<endl;

 for(int j=0;j<(i-1);j++)
  {
   cout<<"* "<<types[j]<<endl;
  }

 fil.close();
}

int checkcode(int code)
{
 fstream fil;
 fil.open( "booklist.dat", ios::in|ios::binary );

 Booklist B;
 int found=0;

 while( fil.read((char*)&B,sizeof(B)) )
  if(B.Rbookcode()==code)
   found++;

 fil.close();

 if(found==0)
  return (0);
 else
  return (1);

}

void returnbook(char username[50])
{
 clrscr();

 int rcode;

 User A;
 fstream fil;
 fil.open("library.dat",ios::in|ios::out|ios::binary);

 int found=0;
 while( fil.read((char*)&A,sizeof(A)) && !found)
	if(strcmp(username,A.Rusername())==0)
	 {
	    found++;

	    if(A.Rnoissued()!=0)
	       {
		cout<<"The books currently issued by you are: "<<endl;
		A.dispissued();
		cout<<endl;
		cout<<"Enter the code of the book you wish to return."<<endl;
		cout<<"Enter 100 if you don't wish to return any book."<<endl;
		cout<<"CODE: ";
		cin>>rcode;

		A.breturn(rcode);
		int pos=( fil.tellg()-sizeof(A) );
		fil.seekg(pos);
		fil.write( (char*)&A,sizeof(A) );
	       }
	    else
	       {
		cout<<"No books issued yet..."<<endl;
		cout<<"Press enter to return to the usermenu"<<endl;
		getch();
		fil.close();
		usermenu(username);
	       }
	 }

fil.close();

 cout<<"Thank you! Keep reading."<<endl;
 cout<<"Press enter to return to user menu.";
 getch();
 usermenu(username);

}

void changepass(char username[50])
{
 clrscr();

 User A;
 fstream fil;
 fil.open("library.dat",ios::in|ios::out|ios::binary);

 int found=0;
 while( fil.read((char*)&A,sizeof(A)) && !found)
	 {
		if(strcmp(username,A.Rusername())==0)
		 {
			found++;
			A.inputnewpass();
			int pos=( fil.tellg()-sizeof(A) );
			fil.seekg(pos);
			fil.write( (char*)&A,sizeof(A) );
		 }
	 }

fil.close();

usermenu(username);
}

void deleteacc(char username[50])
{
 clrscr();

 User A;
 fstream fil;
 fil.open("library.dat",ios::in|ios::out|ios::binary);

 int found=0;
 while( fil.read((char*)&A,sizeof(A)) && !found)
	 {
		if(strcmp(username,A.Rusername())==0)
		 {
			found++;

			int Noissued;
			Noissued=A.Rnoissued();

			if(Noissued>0)
			 {
	fil.close();
	cout<<"You cannot delete your account without returning all the books."<<endl;
	cout<<"Press enter to return to the user menu.";
	getch();
	usermenu(username);
			 }
			else
			 {
	fil.close();

	fstream fil1,fil2;
	fil1.open("library.dat",ios::in|ios::binary);
	fil2.open("temp.dat",ios::out|ios::binary);

	User B;
	int deleted=0;

	while( fil1.read( (char*)&B,sizeof(B) ) )
	 {
		if(strcmp(B.Rusername(),username)==0)
		 deleted++;
		else
		 fil2.write( (char*)&B,sizeof(B) );
	 }

	remove("library.dat");
	rename("temp.dat","student.dat");

	fil1.close();
	fil2.close();

	cout<<"Your account has been deleted."<<endl;
	cout<<"Press enter to return to main menu";
	getch();

	mainmenu();
			 }
	 }
}

}

void showissued(char username[50])
{
 clrscr();

 User A;
 fstream fil;
 fil.open("library.dat",ios::in|ios::out|ios::binary);

 int found=0;
 while( fil.read((char*)&A,sizeof(A)) && !found)
	{
	 if(strcmp(username,A.Rusername())==0)
		{
		 found++;
		 A.dispissued();
		}
	}

 fil.close();

 cout<<"Press enter to return to the user menu.";
 getch();
 usermenu(username);

}

void admincheck()
{
 clrscr();

 char  name[50],pass[50];

 cout<<"Welcome ADMIN"<<endl;
 cout<<"Enter your username: ";gets(name);

 if(strcmp(name,"admin")==0)
	{
	 int count=0;
	 while( strcmp(pass,"password")!=0 && count<=2 )
		{
			cout<<3-count<<" chances left."<<endl;
			cout<<"Enter your password: ";

			int i=0;
			char in;
			do
			{
			 in=getch();
			 if(in!=(char)13)
			 {
				cout<<"*";
				pass[i++]=in;
			 }
			}while(in!=(char)13);
			pass[i]='\0';

			count++;
			cout<<endl;
		}

	 if(count==3)
		{
		 cout<<"Not the admin? press enter to go back to main menu.";
		 getch();
		 mainmenu();
		}
	 else
		{
			adminmenu();
		}
	}
 else
	{
	 cout<<"Username does not exist..."<<endl;
	 cout<<"Press enter to go back to mani menu.";
	 getch();
	 mainmenu();
	}

}

void adminmenu()
{
 clrscr();

 char choice;

 clrscr();
 cout<<"Welcome Admin"<<endl;
 cout<<"ADMIN MENU:"<<endl<<endl;
 cout<<"A.Add a new book."<<endl;
 cout<<"B.Remove a existing book."<<endl;
 cout<<"C.View user list."<<endl;
 cout<<"D.View user info."<<endl;
 cout<<"E.Sign out"<<endl;
 cout<<"F.Reset Library."<<endl;
 cout<<"G.View Book List"<<endl;
 cout<<"H.Edit Book Record"<<endl;
 cout<<"choose a option: ";
 cin>>choice;

 switch (choice)
	{
	 case 'A':
	 case 'a': newbook();
			 break;

	 case 'B':
	 case 'b':removebook();
			break;

	 case 'C':
	 case 'c':viewuserlist();
			break;

	 case 'D':
	 case 'd':viewuserinfo();
			break;

	 case 'E':
	 case 'e': clrscr();
			 cout<<"Press enter to sign out."<<endl;
			 mainmenu();
			 break;

	 case 'F':
	 case 'f':resetlib();
			break;

	 case 'G':
	 case 'g':viewbooklist("admin");
			break;

	 case 'H':
	 case 'h':editrecord();
			break;

	 default :cout<<"Option not Valid."<<endl<<"Press enter to go back.";
			getch();
			adminmenu();
	 }

}

void newbook()
{
 clrscr();

 fstream fil;
 fil.open("booklist.dat",ios::app|ios::binary);

 Booklist B;
 char choice;

 do
 {

	clrscr();

	cout<<"Please provide the required information: "<<endl;
	B.addbook();
	fil.write( (char*)&B,sizeof(B) );

	cout<<"the book has been successfully added."<<endl;
	cout<<"Do you wish to add another book?(y/n)"<<endl;

	cin>>choice;

 }while(choice=='y');

 fil.close();

 clrscr();
 cout<<"Press enter to return to the adminmenu.";
 getch();
 adminmenu();

}

void removebook()
{
 clrscr();

 char choice;
 int fcode,deleted=0;

 choosebook();
 cout<<"Enter the code of the book you wish to remove: "<<endl;
 cin>>fcode;

 Booklist B;
 fstream fil1;
 fil1.open("booklist.dat",ios::in|ios::out|ios::binary);

 while( fil1.read( (char*)&B,sizeof(B) ) && deleted==0)
	{
	 if( fcode==B.Rbookcode() )
		{
		 B.removebook();
		 deleted++;
		 int pos=( fil1.tellg()-sizeof(B) );
		 fil1.seekg(pos);
		 fil1.write( (char*)&B,sizeof(B) );

		}
	}


 fil1.close();

 if(deleted==1)
	{
	 cout<<"The book has been deleted."<<endl;
	 cout<<"Press enter to return to admin menu";

	 getch();
	 adminmenu();
	}
 else
	{
	 cout<<"You have entered an invalid code."<<endl;
	 cout<<"Press enter to return to the admin menu.";
	 getch();
	 adminmenu();
	}
}

void viewuserlist()
{

 clrscr();

 fstream fil;
 fil.open("library.dat",ios::in|ios::binary);

 User A;
 int count=1;

 while(  fil.read((char*)&A,sizeof(A))  )
	cout<<count++<<":"<<A.Rusername()<<endl;

 fil.close();

 cout<<"Press enter to go back.";
 getch();
 adminmenu();

}

void viewuserinfo()
{

 clrscr();

 fstream fil;
 fil.open("library.dat",ios::in|ios::binary);

 User A;
 char name[50];
 int found=0;

 cout<<"Enter the name of the user whose info you wish to view."<<endl;
 gets(name);


 while(  fil.read((char*)&A,sizeof(A)) && found==0 )
	if(strcmp(name,A.Rusername())==0)
		{
		 found++;
		 A.userinfo();
		}

 if(found==0)
	cout<<"Username invalid."<<endl;

 fil.close();

 cout<<"Press enter to go back.";
 getch();
 adminmenu();

}

void resetlib()
{
 cout<<"ARE YOU SURE YOU WANT TO RESET THE LIBRARY?"<<endl;
 cout<<"YOU WILL LOSE ALL SAVED INFORMATION"<<endl;
 cout<<"y/n"<<endl;
 cout<<"Your choice: ";

 char ch;
 cin>>ch;

 if(ch=='y' || ch=='Y')
  {
   remove("library.dat");
   initialize();
  }

 adminmenu();
}

void viewbooklist(char back[80])
{
	char choice='y';
	int code;

	clrscr();

	fstream fil;
	fil.open("booklist.dat", ios::in | ios::binary);
	Booklist B;

	int i=1;

	while( fil.read( (char*)&B,sizeof(B) ) && choice=='y')
	 {
		if(B.Rbookcode()!=100)
		 {
		  cout<<i<<": "<<B.Rbookcode()<<":"<< B.Rbookname() <<" by "<<B.Rbookauthor()<<endl;
		  i++;
		 }
		if(i==16)
		 {
			  cout<<"Do you wish to see more books?(y/n): ";
			  cin>>choice;
			  clrscr();
		 }

	 }

	fil.close();

	if( strcmpi(back,"admin")==0 )
	 {
	  cout<<"Press enter to return to the admin menu";
	  getch();
	  adminmenu();
	 }
	else if( strcmpi(back,"user")==0 )
	 {
	  cout<<"Press enter to proceed to issue the book: "<<endl;
	  getch();
	 }
}
     /* char choice='y';
	int code;

	clrscr();

	fstream fil;
	fil.open("booklist.dat", ios::in | ios::binary);
	Booklist B;

	int i=1;

	while( fil.read( (char*)&B,sizeof(B) ) && choice=='y')
	 {
		if(B.Rbookcode()!=100)
		 {
		  cout<<i<<": "<<B.Rbookcode()<<":"<< B.Rbookname() <<" by "<<B.Rbookauthor()<<endl;
		  i++;
		 }
		if(i==16)
		 {
			  cout<<"Do you wish to see more books?(y/n): ";
			  cin>>choice;
			  clrscr();
		 }

	 }

	fil.close();

	if( strcmpi(back,"admin")==0 )
	 {
	  cout<<"Press enter to return to the admin menu";
	  getch();
	  adminmenu();
	 }
	else if( strcmpi(back,"user")==0 )
	 {
	  cout<<"Press enter to proceed to issue the book: "<<endl;
	  getch();
	 }
       */



void editrecord()
{
 clrscr();

 int code,found=0,run=1;

 cout<<"You can edit the name of the book, author of the book, or the type of the book."<<endl;
 cout<<"Select the book you wish to make changes to: "<<endl;

 choosebook();

 cout<<"Enter the code of the book you wish to edit: ";
 cin>>code;

 if(checkcode(code)==1)
  {
   fstream fil;
   fil.open("booklist.dat",ios::binary|ios::out|ios::in);

   Booklist B;
   char ch;

   while( found==0 && fil.read( (char*)&B,sizeof(B) ) )
    if(code==B.Rbookcode())
     {
      found++;

      clrscr();

      cout<<"EDITING THE BOOK INFO."<<endl<<endl;

      cout<<"The current information of the book is: "<<endl;
      B.displaybook();

      cout<<"What do you want to edit? "<<endl;
      cout<<"A.Book name."<<endl;
      cout<<"B.Book author."<<endl;
      cout<<"C.Book type."<<endl;
      cout<<"D.No change needed."<<endl;
      cin>>ch;
      cout<<endl;

      switch(ch)
       {
	case 'A':
	case 'a': B.Editbookname();
		  break;

	case 'B':
	case 'b': B.Editbookauthor();
		  break;

	case 'C':
	case 'c': B.Editbooktype();
		  break;

	case 'd':
	case 'D': fil.close();
		  run=0;
		  cout<<"No changes have been made."<<endl;
		  cout<<"Press enter to return to the adminmenu."<<endl;
		  getch();

		  adminmenu();

		  break;

	default : cout<<"Invalid choice"<<endl;
		  cout<<"Press enter to go back.";
		  run=0;
		  getch();
		  fil.close();
		  adminmenu();

       }

       int pos=( fil.tellg()-sizeof(B) );
       fil.seekg(pos);
       fil.write( (char*)&B,sizeof(B) );

      }

      if(found==1 && run==1)
       {
	cout<<"The requested change has been make."<<endl;
	cout<<"Press enter to go back.";
	fil.close();
	getch();
	adminmenu();
       }

     }
    else
     {
      cout<<"You entered an invalid code."<<endl;
      cout<<"Press enter to go back";
      getch();

      adminmenu();
     }

}

void initialize()
{
 fstream fil;
 fil.open("booklist.dat",ios::out|ios::binary);

 Booklist A("1984","A","Science Fiction",101),
		B("Time Machine","H.G.Wells","Science Fiction",102),
		C("I-Robot","Ian","Science Fiction",103),
		D("Hitchhiker's Guide to the Galaxy","A","Science Fiction",104),
		E("Frankenstein","A","Science Fiction",105),
		F("Gone Girl","A","Mystery",201),
		G("Angels & Demons","Dan Brown","Mystery",202),
		H("Sherlock Holmes","Conan Doyle","Mystery",203),
		I("Gone Tommorrow","Lee Child","Mystery",204),
		J("And Then There Were None","Agatha Cristine","Mystery",205),
		K("Paper Lion","A","Sports",301),
		L("Into Thin Air","A","Sports",302),
		M("Eight Men Out","A","Sports",303),
		N("Friday Night Lights","A","Sports",304),
		O("The Game","A","Sports",305),
		P("Pride & Prejudice","Jane Austin","Romance",401),
		Q("Gone With The Wind","A","Romance",402),
		R("Wuthering Heights","A","Romance",403),
		S("Jane Eyre","Jane Austin","Romance",404),
		T("Sense & Sensibility","A","Romance",405),
		U("Leviathan Wakes","A","Adventure",501),
		V("Use of Weapons","A","Adventure",502),
		W("Uncharted Territories","A","Adventure",503),
		X("Deathworld","A","Adventure",504),
		Y("The Hunger Games","Susan Collins","Adventure",505);

 fil.write((char*)&A,sizeof(A));
 fil.write((char*)&B,sizeof(A));
 fil.write((char*)&C,sizeof(A));
 fil.write((char*)&D,sizeof(A));
 fil.write((char*)&E,sizeof(A));
 fil.write((char*)&F,sizeof(A));
 fil.write((char*)&G,sizeof(A));
 fil.write((char*)&H,sizeof(A));
 fil.write((char*)&I,sizeof(A));
 fil.write((char*)&J,sizeof(A));
 fil.write((char*)&K,sizeof(A));
 fil.write((char*)&L,sizeof(A));
 fil.write((char*)&M,sizeof(A));
 fil.write((char*)&N,sizeof(A));
 fil.write((char*)&O,sizeof(A));
 fil.write((char*)&P,sizeof(A));
 fil.write((char*)&Q,sizeof(A));
 fil.write((char*)&R,sizeof(A));
 fil.write((char*)&S,sizeof(A));
 fil.write((char*)&T,sizeof(A));
 fil.write((char*)&U,sizeof(A));
 fil.write((char*)&V,sizeof(A));
 fil.write((char*)&W,sizeof(A));
 fil.write((char*)&X,sizeof(A));
 fil.write((char*)&Y,sizeof(A));

 fil.close();

}


