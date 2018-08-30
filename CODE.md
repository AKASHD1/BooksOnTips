# BooksOnTips
// concepts of oops- Library management system
#include<iostream>
#include<ctime>
using namespace std;

class student{
	public:
	static int srollno;
	int rollno;                   //take lib id instead of roll no if you only want to use static members
	string name;
	string department;
	char section;
	char semester;
	int no_of_books;
	
		student()
		{
			rollno=srollno;
			srollno++;
		}
		void input_student()
		{
			cout<<"\nEnter the details of the student";
			cout<<"\nRoll no of the student:";cout<<rollno;
			cout<<"\nEnter the name of the student:";cin>>name;
			cout<<"\nEnter department of the student:";cin>>department;
			cout<<"\nEnter the section of the student:";cin>>section;
			cout<<"\nEnter the semester of the student:";cin>>semester;
		}
		void display_student()
		{
			cout<<"\nDetails of the student";
			cout<<"\nroll no of the student:";cout<<rollno;
			cout<<"\nname of the student:";cout<<name;
			cout<<"\ndepartment of the student:";cout<<department;
			cout<<"\nEnter the section of the student:";cout<<section;
			cout<<"\nEnter the semester of the student:";cout<<semester;
		}
		 void register_student(student s)
  		{
           input_student();
		   display_student();	
		 }
};
int student::srollno = 100;
class book{
	public:
	int bookid;
	string author;
	string title;
		
		void input_book()
		{
			cout<<"\nEnter the details of the book";
			cout<<"\nEnter the id of book:";cin>>bookid;
			cout<<"\nEnter the author of the book:";cin>>author;
			cout<<"\nEnter title of the book:";cin>>title;
			
		}
		void display_book()
		{
			cout<<"\nDetails of the book";
			cout<<"\nId of book:";cout<<bookid;
			cout<<"\nAuthor of the book:";cout<<author;
			cout<<"\nTitle of the book:";cout<<title;
		}
		 void register_book(book b)
  {
           	input_book();
           	display_book();
 }
	
};

class record
{
	public:
	int roll;
	int bookid;
	string return_date;
	string issue_date;
	
		 make_record(int x, int y)
		{
			roll=x;
			bookid=y;             //we can use this pointer here too.
		}
	void func_issue_date()
	{
		//declaring argument for time
	time_t tt;
   // Declaring variable to store return value of
    // localtime()
    struct tm * ti;
 
    // Applying time()
    time (&tt);
 
    // Using localtime()
    ti = localtime(&tt);
 
    cout << "\nIssued Day, Date and Time is = "
         << asctime(ti);
	issue_date=asctime(ti);	
	}
	
	void actual_ret_date()
	{
		cout<<"\nYou have to return the book within 21 days.";
	}
	
	void func_ret_date()
	{
		//declaring argument for time
	time_t tg;
   // Declaring variable to store return value of
    // localtime()
    struct tm * ti;
 
    // Applying time()
    time (&tg);
 
    // Using localtime()
    ti = localtime(&tg);
 
    cout << "\nReturning Day, Date and Time is = "
         << asctime(ti);
	return_date=asctime(ti);		            //now find fine.
	}     	
};
void calculate_fine(int days)
{
	if(days>21)
	{
		cout<<"\n Your Fine amount: RS"<<((days-21)*5);
		cout<<"\n Be regular from next time ";
	}
	else
	{
		cout<<"\n You have no fine.";
	}
}
 //to search record
    void search_record(int sel_roll,int sel_book,record r[],int count)
 {
 	int found=-1;
 	for(int i=0;i<=count;i++)
 	{
 		if((sel_book==r[i].bookid)&&(sel_roll=r[i].roll))
 		{
 			found=i;
 			break;
		 }
	}
	if(found==-1)
	{
		cout<<"\nRecord not found!";
	}
	else
	{	
	r[found].bookid=0;
	r[found].roll=0;
	 r[found].func_ret_date();
	 cout<<"\nNo of days the student kept the book:";
	 int finedays;                                          //have to complete this part.
	 cin>>finedays;
	 calculate_fine(finedays);
	 cout<<"\n\nYour book has been returned.";
 	}
 }
 
 void return_book(record r[],int count)    
 {
 	int sel_roll,sel_book;
 	cout<<"\nEnter student roll no:";
	cin>>sel_roll;
	cout<<"\nEnter ID of the book you want to return: ";
	cin>>sel_book;
	search_record(sel_roll,sel_book,r,count);
 }  

  void issue_book(record r[],int count)
 { int sel_roll,sel_book;
 	cout<<"\nEnter student roll no:";
cin>>sel_roll;
cout<<"\nEnter ID of the book you want to issue: ";
cin>>sel_book;
r[count].make_record(sel_roll,sel_book);
r[count].func_issue_date();
r[count].actual_ret_date();
cout<<"\nYour book has been issued.";
 }

int main()
{
	student s[500];    //array of student objects
	book b[500];       //array of book objects
	record r[100];    //array of records
	int nos=1;        //no of students
	char check;
	int sel,count1=0,count2=0,count3=0;
		cout<<"******************library*********************";
	do{
cout<<"\nEnter your choice:";
cout<<"\n1.Want to return book";
cout<<"\n2.Want to issue book";
cout<<"\n3.Want to register a student";
cout<<"\n4.Want to register a book";
cout<<"\n\nEnter your selection:";
cin>>sel;
int sel_roll;

switch(sel)
{
 case 1:return_book(r,count3);
 			break;
 case 2:issue_book(r,count3);
 			break;
 case 3:s[count1].register_student(s[count1]);
           count1++;
 			break;
 case 4:b[count2].register_book(b[count2]);
 			count2++;
 			break;			
 default: cout<<"\nEnter a valid choice.";	
}
cout<<"\n\nWant to perform another operation.(Y/N)";
cin>>check;	
}while((check=='Y')||(check=='y'));
cout<<"\n\nThank you and Do visit us again!";
return 0;
	
}
