#include<iostream.h>
#include<conio.h>
#include<fstream.h>
#include<stdio.h>
#include<string.h>
#include<process.h>
#include<dos.h>
#include<time.h>
#include<iomanip.h>

//food.dat for data contains all the dishes
//userdata.dat contains users data

int id=0;
void decrease_dish_quantity();
void display_dish();
void display_orders(int);
void rate_dish();
void write_data();
void track_orders();
void add_to_cart();
void admin();
void User();
void add_dish();
void delete_dish();
void modify();
void view_rating();
void buy_dish();
void heading();

struct cart_item
{ //for one item of the cart
    char dishname[40];
    float cost;
    int quantity;
    int rating;
//add rating
}item;

class order
{ //for an order of a user
    int order_id;
    long int phonenumber; // for user id
    cart_item cart[10]; //cart array
    int cart_items; //number of items in cart
    float grandtotal;
    time_t order_time; //time_t is a datatype for time related operations

    public:
     void display();
     void place(cart_item source_cart[10], int source_cart_items, float total, long int phoneno,int id)
    {
	memcpy(cart,source_cart,sizeof(cart_item)*source_cart_items); //copy user cart to order cart
	//copies code from source to this destination
	cart_items=source_cart_items;
	phonenumber = phoneno;
	grandtotal = total;
	order_time = time(NULL);

	order_id=id;
    }
    time_t get_order_time()
    {
	return order_time;
    }

    long int get_phoneno()
    {
	return phonenumber;
    }
    int get_id()
	{
	return order_id;
	}
} order1;
void order::display()
{
		cout<<"ORDER: "<<order_id<<endl;
		cout<<"TIME: "<<asctime(localtime(&order_time));
		cout<<setw(20)<<"DISH NAME : "<<setw(20)<<" COST : "<<setw(20)<<" QUANTITY : "<<setw(20)<<" RATING : "<<endl;
		for(int i=0;i<cart_items;i++)
		{
			cout<<setw(15)<<cart[i].dishname<<setw(20)<<"Rs."<<cart[i].cost<<setw(20)<<cart[i].quantity<<setw(15)<<cart[i].rating<<endl;
		}
		cout<<"GRAND TOTAL :Rs."<<grandtotal;
		getch();
}
class dish
{
    char dishname[100];//name of dish
    float cost;//cost of dish
    int rating;//rating of dish
    int quantity;//number of dish in supply left
    int total_ratings;//number of ratings dish has received
    char category[20]; //stores the category name
    public:
    char* get_dishname()
    {
	return dishname;
    }

    float get_cost()
    {
	return cost;
    }
    char* get_category()
    {
	return category;
    }
    int get_quantity()
    {
	return quantity;
    }
   /* int put_quantity()
    {
    } */

    int get_rating()
    {
	return rating;
    }

    int get_total_ratings()
    {
	return total_ratings;
    }

    void initial_rating()
    {
	total_ratings=0;
	rating=0;
    }
    void newquantity(char choice[12],int user_quantity)
    {   if(strcmp(choice,"cart_del")==0)         //cart_del if user deletes a dish from their cart, supply increase
	quantity+=user_quantity;
	else if(strcmp(choice,"cart_add")==0)    //cart_add if user adds dish to cart
	quantity-=user_quantity;
    }

     void rating1(int user_rating)
    {
		rating=((rating*total_ratings) + user_rating)/(total_ratings+1); //after first rating
		total_ratings++;
    }

    void fill(); //defined below

    void set_name()
    {
	cout<<"ENTER DISH NAME :";
	gets(dishname);
    }

    void set_cost()
    {
	cout<<"\nENTER DISH COST :";
	cin>>cost;
    }

    void set_quantity()
    {
	cout<<"\nENTER QUANTITY:";
	cin>>quantity;
    }

    void set_quantity(int qty)
    {
	quantity = qty;
    }

    void display()
    {
	cout<<"DISHNAME: "<<dishname<<endl;
	cout<<"COST: "<<cost<<endl;
	cout<<"QUANTITY: "<<quantity<<endl;
	cout<<"CATEGORY: "<<category<<endl;
	cout<<"RATING: "<<rating<<" (OUT OF 5)"<<endl;
    }
    void add_category();

} b1,b2;//end of class book
void dish::fill()
    {
	cout<<"ENTER DISH NAME :";
	gets(dishname);
	cout<<"\nENTER DISH COST :";
	cin>>cost;
	do
	{
		cout<<"\nENTER QUANTITY:";
		cin>>quantity;
		if(quantity<0)
		{
			cout<<"ERROR : CANNOT BE NEGATIVE"<<endl;
		}
	}
	while(quantity<0);
	cout<<"\nENTER CATEGORY:";
	add_category();
	initial_rating();
    }

void dish::add_category()
{
	int choice;
	cout<<"\n1.German \n2.Indian \n3.Japanese \n4.Italian \n5.Others"<<endl;
	cin>>choice;
	switch(choice)
	{
		case 1:
		strcpy(category,"German");
		break;
		case 2:
		strcpy(category,"Indian");
		break;
		case 3:
		strcpy(category,"Japanese");
		break;
		case 4:
		strcpy(category,"Italian");
		break;
		case 5:
		strcpy(category,"Others");
		break;
		default:
		cout<<"WRONG CHOICE.";
	 }
    }
class user
{
    char username[40];
    char address[100];
    long int phonenumber; //treated as user id (Primary key)
    char password[40];
    cart_item cart[10]; //cart array
    int cart_items; //number of items in cart

    public:

    char* get_username()
    {
	return username;
    }

    int get_cart_items()
    {
	return cart_items;
    }

    char* get_address()
    {
	return address;
    }

    long int get_phoneno()
    {
	return phonenumber;
    }

    char* get_password()
    {
	return password;
    }

    void setcart()
    { //sets cart items to 0 when user signs up
	cart_items=0;
    }
    cart_item get_cart(int t)
    {
	return cart[t];
    }
    int get_items()
    {
	return cart_items;
    }

    void empty_cart(int);
    void add_to_cart();
    void fill();
    void delete_item();
    void display_cart();
    void place_order();
    void change_itemquantity();
} user1, loggedin_user;
//used to store info of the logged in user and to later search for his record to modify
//end of class user
void user::add_to_cart()
{
	cart[cart_items]=item;
	cart_items++;//increase items of cart by 1

}
void user::fill()
{

	cout<<"ENTER USER NAME : ";
	gets(username);
	cout<<"\nENTER PHONE NUMBER (10 DIGITS):  ";
	cin>>phonenumber;
	cout<<"\nENTER ADDRESS:";
	gets(address);
	cout<<"\nENTER PASSWORD :";
	gets(password);
}
void user::display_cart()
{
       cout<<setw(20)<<"|DISH NAME "<<setw(20)<<" |QTY "<<setw(20)<<" |COST  Rs."<<endl;

	for(int i=0;i<cart_items; i++)
	{
		cout<<(i+1)<<": ";
		cout<<setw(15)<<cart[i].dishname<<setw(20)<<cart[i].quantity<<setw(20)<<cart[i].cost<<endl;
	}
}
void user::change_itemquantity()
{
 char name[50];
 int newquantity;
 if(cart_items==0)
	{
	    cout<<setw(10)<<"CART IS EMPTY"<<endl;
	    return;
	}
	dish o1;
	fstream fin3("dish.dat",ios::binary|ios::in);
	fstream fout3("D.dat",ios::binary|ios::out);

	if(!fout3||!fin3)
	{
		cout<<setw(10)<<"MENU NOT WORKING. PLEASE TRY LATER.";
		return;
	}
	int flag=-1;
	cout<<setw(10)<<"ENTER NAME OF DISH WHOSE QUANTITY YOU WANT TO CHANGE:"<<endl;
	gets(name);
	for(int i=0;i<cart_items;i++)
	{

	    if(strcmp(cart[i].dishname,name)==0)
	     {


		flag++;
		cart_item temp;
		temp=cart[i];
		cout<<setw(10)<<"CURRENT QUANTITY :"<<cart[i].quantity<<endl;
		qty:
		cout<<setw(10)<<"ENTER NEW QUANTITY:(>0) ";
		cin>>newquantity;
		if(newquantity<=0)
		   {
			cout<<"INVALID ENTRY! PLS TRY AGAIN"<<endl;
			goto qty;
		   }

		cart[i].quantity=newquantity;
		while(fin3.read((char*)&o1,sizeof(o1)))
		{
			if(strcmp(o1.get_dishname(),name)==0)
			{
				if(newquantity>(o1.get_quantity()+temp.quantity))
				{
					cout<<setw(10)<<"QUANTITY ENTERED IS MORE THAN QUANITY IN STORE."<<endl;
					cart[i].quantity=temp.quantity;

				}
				else
				{
				if(temp.quantity>cart[i].quantity)
				{
				 o1.newquantity("cart_del",(temp.quantity-cart[i].quantity));
				}
				else if(temp.quantity<cart[i].quantity)
				{
					 o1.newquantity("cart_add",(cart[i].quantity-temp.quantity));
				}
			}
		       }
		       fout3.write((char*)&o1,sizeof(o1));
		 }
	   }
	   }
	   fin3.close();
	   fout3.close();
	   remove("dish.dat");
	   rename("D.dat","dish.dat");
       if(flag==-1)
	 cout<<setw(10)<<"DISH NOT FOUND IN CART.";
}
void user::delete_item()
{
	if(cart_items==0)
	{
	    cout<<"CART IS EMPTY"<<endl;
	    return;
	}
	dish o1;
	fstream fin("dish.dat",ios::binary|ios::in);
	fstream fout("D.dat",ios::binary|ios::out|ios::app);
	if(!fout||!fin)
	{
		cout<<"MENU NOT WORKING. PLEASE TRY TO DELETE ITEMS LATER.";
		return;
	}
	int flag=-1;
	char name[50];
	cout<<"ENTER NAME OF THE DISH YOU WANT TO DELETE"<<endl;
	gets(name);
	for(int i=0;i<cart_items;i++)
	{
	    if(strcmp(cart[i].dishname,name)==0)
	     {
		flag++;
		cart_item temp;
		temp=cart[i];
		cart[i]=cart[cart_items-1];
		cart[cart_items-1]=temp;
		cart_items--;
		while(fin.read((char*)&o1,sizeof(o1)))
		{
			if(strcmp(o1.get_dishname(),name)==0)
			{
			       o1.newquantity("cart_del",temp.quantity);
			       fout.write((char *)&o1,sizeof(o1));
			}
			else
				fout.write((char*)&o1,sizeof(o1));
		}
		fin.close();
		fout.close();
		remove("dish.dat");
		rename("D.dat","dish.dat");
	  }
	}
	 if(flag==-1)
	 cout<<"DISH NOT FOUND IN CART.";

}

void user::empty_cart(int mode = 0)
{
// 0:empty, place
    int temp = cart_items;
    cart_items = 0;
    if(mode==1) return;
    dish o1;
    for(int i = 0; i < temp; i++)
    {
	fstream fout("D.dat",ios::binary|ios::out|ios::app);
	fstream fin("dish.dat",ios::binary|ios::in);
	while(fin.read((char*)&o1,sizeof(o1)))
	{
	    if(strcmp(o1.get_dishname(),cart[i].dishname)==0)
	    {
		o1.newquantity("cart_del",cart[i].quantity);
		fout.write((char *)&o1,sizeof(o1));
	    }
	    else
		fout.write((char*)&o1,sizeof(o1));
	}
	fin.close();
	fout.close();
	remove("dish.dat");
	rename("D.dat","dish.dat");
    }
}
void user::place_order()
{
	float grandtotal=0;
	float total_cost=0;

	for(int i=0;i<cart_items;i++)
	{
	    total_cost += cart[i].cost*cart[i].quantity;
	}
	float tax=(0.1)*total_cost;
	grandtotal=total_cost+tax;
	cout<<endl<<"TOTAL COST: Rs."<<total_cost<<endl;
	cout<<"TOTAL TAX: Rs."<<tax<<endl<<endl;
	cout<<"GRAND TOTAL: Rs."<<grandtotal<<endl;
	fstream fout("orders.dat",ios::app|ios::binary); //to get id of placed order
	if(!fout)
	{
		cout<<"ERROR IN PLACING ORDER"<<endl;
	    return;
	}
	fout.seekg(0,ios::end);
	id=fout.tellg()/sizeof(order1);
	id=id+1;
	cout<<"\nYOUR ORDER ID :"<<id<<endl;
	order1.place(cart,cart_items,grandtotal,phonenumber,id);
      fout.write((char*)&order1,sizeof(order1));
      fout.close();
}
void add_to_cart()
{
    loggedin_user.add_to_cart();
}

void display_orders(int mode = 0)
{
    fstream fin("orders.dat",ios::in|ios::binary | ios::out);
    if(!fin)
    {
		cout<<"ERROR IN DISPLAYING ORDERS";
		return;
    }
    //0:user, 1:admin
    int flag=-1;//to validate phone in admin
    int flag2=-1;  //to check if user has any orders
    if(mode == 0)
    {
	while(fin.read((char*)&order1,sizeof(order1)))
	{
		if(order1.get_phoneno()==loggedin_user.get_phoneno())
		{
			flag2++;
			order1.display();
			cout<<endl;
		}
	}

	  if(flag2==-1)
	      cout<<"NO PREVIOUS ORDERS!"<<endl;

    }
    else
	{
		long int phoneno;
		cout<<"ENTER PHONE NUMBER OF USER"<<endl;
		cin>>phoneno;

		while(fin.read((char*)&order1,sizeof(order1)))
		{
			if(order1.get_phoneno()==phoneno)
			{
				flag++;
				order1.display();
				cout<<endl;
			}
		}
			if(flag==-1)
		  cout<<"USER NOT FOUND"<<endl;
	}

    getch();
    fin.close();
}

void view_cart()
{ //to display cart

	if(loggedin_user.get_cart_items()==0)
	{
	    cout<<"EMPTY CART !"<<endl;
	    return;
	}
	//cart menu
	do {
	    clrscr();
	     cout<<"\t\t\t\tCART ITEMS"<<endl;
	     loggedin_user.display_cart();

	     cout<<endl;

	    cout<<"1.DELETE ITEM FROM CART"<<endl;
	    cout<<"2.EMPTY CART"<<endl;
	    cout<<"3.CHANGE QUANITY OF ITEM"<<endl;
	    cout<<"4.PLACE ORDER AND CHECKOUT"<<endl;
	    cout<<"5.EXIT CART"<<endl;
	    char ch;//choice
	    cout<<endl<<"CHOOSE YOUR OPTION:";
	    cin>>ch;
	    cout<<endl;
	    switch(ch)
	    {
		case '1': loggedin_user.delete_item();
			getch();
			if(loggedin_user.get_cart_items()==0)
			    return;
			break;
		case '2': loggedin_user.empty_cart();
			getch();
			return;
		case '3':
			loggedin_user.change_itemquantity();
			return;
		case '4':
			loggedin_user.place_order();
			loggedin_user.empty_cart(1);
			cout<<"YOUR ORDER HAS BEEN PLACED. THANK YOU FOR ORDERING!"<<endl;
			cout<<"YOUR FOOD IS ON IT'S WAY"<<endl;
			getch();
			return;
		case '5': return;
		default: cout<<"WRONG CHOICE ! ENTER AGAIN"<<endl;
	    }
	} while(1);
}

void password(char pass[])
{ //renaming the input variable to avoid confusion
    int i=0; //loop counter
    char temp; //a Temp char
    for(i=0; ; )
    { //infinite loop
	temp=getch(); //stores char typed in temp
	if((temp>='a'&&temp<='z')||(temp>='A'&&temp<='Z')||(temp>='0'&&temp<='9'))
	{
	//check if a is numeric or alphabet
	    pass[i]=temp; //stores temp in pass
	    ++i;
	    cout<<"*";
	}
	if(temp=='\b'&& i>=1)
	{//if user typed backspace
	//i should be greater than 1.
	    cout<<"\b \b"; //delete the character behind the cursor.
	    --i;
	}
	if(temp=='\r')
	{//if enter is pressed
	    pass[i]='\0'; //null means end of string.
	     break; //break the loop
	}
    }
} //end of password function

void login()
{
	cout<<endl;
    cout<<"1.LOGIN AS ADMINISTRATOR"<<endl;
    cout<<"2.LOGIN AS USER"<<endl;
    cout<<endl<<"ENTER CHOICE:";
    char choice;
    cin>>choice;
    cout<<endl;
    char admin_password[50];
    switch(choice)
    {
	case '1':
			cout<<"ENTER PASSWORD"<<endl;
			int admin_attempts=3;
			while(admin_attempts>0)
			{
			admin_attempts--;
			password(admin_password);
			if(strcmp(admin_password,"iamdish")==0)
			{
			    admin(); //calls admin function which handles all operations of admin
			    return;
			}
			else
			{
				cout<<"\nINCORRECT PASSWORD! TRY AGAIN!"<<endl;
				cout<<admin_attempts<<" attempts left!"<<endl;
			}
			}
		    if(admin_attempts==0)
		    {
			cout<<"SHUTTING DOWN!"<<endl;
			getch();
			exit(0);
		    }
		    break;

	case '2':   long int phone;
		    char pass[40]; //temporary variable to store entered password
		    int attempts=3;
		    while(attempts>0)
		    {
			fstream fin("userdatabase.dat", ios::binary|ios::in|ios::out);
			if(!fin)
			{
				cout<<"ERROR IN OPENING FILE"<<endl;
				return;
			}
			cout<<"ENTER YOUR PHONE NUMBER  AND PASSWORD"<<endl;
			cout<<"PHONE NO :";
			cin>>phone;
			cout<<"PASSWORD :";
			password(pass);
			attempts--;
			while(fin.read((char*)&user1,sizeof(user1)))
			{
			    if((user1.get_phoneno()==phone) && strcmp(user1.get_password(),pass)==0)
			     {

					cout<<"\nLOGIN SUCCESSFUL! PRESS ANY KEY TO CONTINUE!"<<endl;
					loggedin_user=user1;
					getch();
					User();
					return;

			    }
			}
			cout<<"\nINCORRECT PHONE NUMBER OR PASSWORD! TRY AGAIN!"<<endl;
			cout<<"You have "<<attempts<<" attempts left!"<<endl;
			fin.close();
		    }//end of attempts loop
		    cout<<"TOO MANY ATTEMPTS! LOGIN FAILED!"<<endl;
		    getch();
    }
} // END OF LOGIN()

void signup()
{
	phone:
	fstream fin("userdatabase.dat",ios::binary | ios::in|ios::out);
	user o1;
	int invalid_ph=0;

	if(!fin)
	{
		cout<<"ERROR IN OPENING FILE"<<endl;
		return;
	}
	 user1.fill();
	 if(!fin)
	 {
		 cout<<"DATABASE NOT WORKING. TRY TO SIGN UP LATER."<<endl;
		 return;
	 }
	 while(fin.read((char*)&o1,sizeof(o1)))
	 {
		if(user1.get_phoneno()==o1.get_phoneno())
		{
			invalid_ph++;
			break;
		}
	 }
	 fin.close();
	 if(invalid_ph==0)
	 {
		ofstream fout("userdatabase.dat", ios::binary | ios::app);
		user1.setcart();
		fout.write((char*)&user1,sizeof(user1));
		fout.close();
		cout<<"\nDATA SUCCESSFULLY SAVED"<<endl;
	 }
	 else
	 {
		     cout<<endl<<"PHONE NUMBER ALREADY REGISTERED. TRY AGAIN!"<<endl;
		     goto phone;
	 }

}//end of signup

void admin()
{
	do {
		clrscr();
		heading();
		cout<<endl;
		cout<<"1.ADD A DISH"<<endl;
		cout<<"2.DELETE A DISH"<<endl;
		cout<<"3.MODIFY DISH DETAILS"<<endl;
		cout<<"4.VIEW RATING"<<endl;
		cout<<"5.VIEW MENU"<<endl;
		cout<<"6.VIEW CUSTOMER ORDERS"<<endl;
		cout<<"7.LOG OUT"<<endl;
		int ch;
		cout<<"ENTER CHOICE: ";
		cin>>ch;
		cout<<endl;
	switch(ch)
	{
	    case 1:
	    {
			add_dish();
			getch();
			break;
	    }
	    case 2:
	    {
			delete_dish();
			getch();
			break;
	    }
	    case 3:
	    {
			modify();
			getch();
			break;
	    }
	    case 4:
	    {
			view_rating();
			getch();
			break;
	    }
	    case 5:
	    {
			display_dish();
			getch();
			break;
	    }
	    case 6: {
			display_orders(1);
			getch();
			break;
	    }
	    case 7:
	    {
		     char choice;
		     cout<<"ARE YOU SURE YOU WANT TO LOG OUT? (Y OR N)"<<endl;
		     label:
		     cin>>choice;
		     if(choice=='y' || choice=='Y')
		     {
				return;
		     }
		     else if(choice=='n'|| choice=='N')
		     {
				break;
		     }
		     else
		     {
			cout<<"WRONG CHOICE! - TRY AGAIN"<<endl;
			goto label;
		     }
	    }
	    default:
	    {
			cout<<"WRONG CHOICE"<<endl;
			getch();
	    }
	}
    } while(1);
} // end of admin()

void User()
{
    do {
	clrscr();
	heading();
	cout<<endl;
	cout<<"\t\t\t   WHAT WOULD YOU LIKE TO DO?"<<endl;
	cout<<"1.BUY FOOD"<<endl;
	cout<<"2.DISPLAY MENU"<<endl;
	cout<<"3.VIEW CART"<<endl;
	cout<<"4.RATE A DISH"<<endl;
	cout<<"5.DISPLAY PREVIOUS ORDERS"<<endl;
	cout<<"6.LOG OUT"<<endl;
	int ch;
	cout<<"ENTER CHOICE"<<endl;
	cin>>ch;//for user menu
	cout<<endl;
	switch(ch) {
	    case 1:     clrscr();
			heading();
			buy_dish();
			getch();
			break;
	    case 2:
			clrscr();
			heading();
			display_dish();
			getch();
			break;
	    case 3:
			clrscr();
			heading();
			view_cart();
			getch();
			break;

	    case 4:
			clrscr();
			heading();
			rate_dish();
			getch();
			break;
	    case 5:
			clrscr();
			heading();
			display_dish();
			getch();
			break;
	    case 6:
			clrscr();
			heading();
			write_data();
			return;
	    default:
			cout<<endl;
			cout<<"INVALID OPTION"<<endl;
			getch();
	}
    } while(1);
} //end of User()

void rate_dish()
{
	char name[50];//book name to be rated
	int rating;
	fstream fin("dish.dat",ios::binary|ios::in);
	fstream fout("temp.dat",ios::binary|ios::out);
	if(!fin||!fout)
	{
		cout<<"ERROR IN OPENING FILE"<<endl;
		return;
	}
	cout<<"ENTER THE NAME OF THE DISH YOU WANT TO RATE"<<endl;
	gets(name);
	while(fin.read((char*)&b1,sizeof(b1)))
	{
		if(strcmpi(b1.get_dishname(),name)==0)
		{
			if(b1.get_rating()==0)
			{
				cout<<"BE THE FIRST TO RATE THIS DISH!"<<endl;
			}
			do{
				cout<<"ENTER NUMERIC RATING (1 to 5)"<<endl;
				cin>>rating;
				if(rating >5)
				{
				   cout<<"INVALID RATING.ENTER A RATING BELOW 5"<<endl;
				}
				else
				{
					cout<<"THANK YOU FOR RATING!"<<endl;
				}
			}while(rating > 5);
			b1.rating1(rating);
		}
		fout.write((char*)&b1,sizeof(b1));
	}
	fin.close();
	fout.close();
	remove("dish.dat");
	rename("temp.dat","dish.dat");
}

void write_data()
{
	fstream fin("userdatabase.dat",ios::binary|ios::in);
	fstream fout("temp.dat",ios::binary|ios::out);
	if(!fin||!fout)
	{
		cout<<"ERROR IN OPENING FILE"<<endl;
		return;
	}
	while(fin.read((char*)&user1,sizeof(user1)))
	{
		if(user1.get_phoneno()==loggedin_user.get_phoneno())
		{
		    user1=loggedin_user;
		}
		fout.write((char*)&user1,sizeof(user1));
	}
	fin.close();
	fout.close();
	remove("userdatabase.dat");
	rename("temp.dat","userdatabase.dat");
}

void add_dish()
{
    int flag=0;
    fstream fin1("dish.dat",ios::binary|ios::in);
    fstream fout("temp.dat",ios::binary|ios::out);
    cout<<"\nENTER DATA:\n";
    b2.fill();
    if(!fout) {
	cout<<"ERROR OPENING FILE"<<endl;
	return;
    }

    //following is adding dish in sorted alphabetical order
    while(fin1.read((char*)&b1,sizeof(b1))) {
	if(strcmp(b1.get_dishname(),b2.get_dishname())<0)
	    fout.write((char*)&b1,sizeof(b1));
	else
	{
	    flag++;
	    fout.write((char*)&b2,sizeof(b2));
	    fout.write((char*)&b1,sizeof(b1));
	    break;
	}
    }
    while(fin1.read((char*)&b1,sizeof(b1)))
    {
	fout.write((char*)&b1,sizeof(b1));
    }
    if(flag==0)
	fout.write((char*)&b2,sizeof(b2));
    fin1.close();
    fout.close();
    cout<<"DISH ADDED"<<endl;
    remove("dish.dat");
    rename("temp.dat","dish.dat");
} //end of add_book()

void delete_dish()
{
	clrscr();
	heading();
	cout<<endl<<"DELETE MENU"<<endl;
	display_dish();
	cout<<endl;

    int flag=0,founddish=0;
    char name[50];//dish to be deleted
    fstream fin1("dish.dat",ios::binary|ios::in);
    fstream fout("temp.dat",ios::binary|ios::out);
    if(!fin1||!fout)
    {
	cout<<"THERE ARE NO DISHES TO BE DELETED."<<endl;
	return ;
    }
    cout<<endl<<"ENTER THE DISH YOU WANT TO DELETE"<<endl;
    gets(name);
    while(fin1.read((char*)&b1,sizeof(b1)))
    {
	if(strcmp(b1.get_dishname(),name)==0)
	{
	    founddish=1;
	    flag++;
	    cout<<"THE DISH BEING DELETED IS :"<<endl;
	    b1.display();
	    continue;
	}
	fout.write((char*)&b1,sizeof(b1));
    }
    if(!founddish)
    {
	cout<<"DISH NOT FOUND"<<endl;
    }
    fin1.close();
    fout.close();
    remove("dish.dat");
    rename("temp.dat","dish.dat");
} //end of delete_dish()

void display_dish()
{ //display books in chosen sorted order
    cout<<"1.DISPLAY IN ALPHABETICAL ORDER"<<endl;
    cout<<"2.DISPLAY IN ORDER OF RATING"<<endl;
    cout<<"3.DISPLAY BY CATEGORY"<<endl;
    cout<<"SELECT YOUR OPTION:";
    int ch;//choice
    cin>>ch;
    cout<<endl;
    fstream fin1("dish.dat", ios::binary | ios::in);
    if(!fin1)
    {
	cout<<"Error in accessing dish!"<<endl;
	return;
    }
    int count=0;
    while(fin1.read((char*)&b1,sizeof(b1)))
    {
	 count=1;//to check if empty
    }
    fin1.close();
    fin1.open("dish.dat",ios::binary|ios::in);
    if(!count)//when file exists but there are no dishes
    {
	cout<<"NO DISHES IN STORE"<<endl;
	return;
    }

    switch(ch)
    {

	case 1:
		cout<<setw(20)<<"|DISH NAME  "<<setw(20)<<" |COST Rs.  "<<setw(20)<<" |QUANTITY  "<<setw(20)<<" |RATING  "<<endl;
		while(fin1.read((char*)&b1,sizeof(b1)))
		{
			cout<<setw(15)<<b1.get_dishname()<<setw(18)<<b1.get_cost()<<setw(20)<<b1.get_quantity();
			if(b1.get_rating()==0)
			   cout<<setw(20)<<"NA";

			else
			{
				int stars=b1.get_rating();
				cout<<setw(20);
				for(int k=1;k<=stars;k++)
				   cout<<"*";
			}
			cout<<endl;
		    }
		    fin1.close();
		    break;
	case 2:
		cout<<setw(20)<<"|DISH NAME "<<setw(20)<<" |COST Rs.  "<<setw(20)<<" |QUANTITY  "<<endl;
		while(fin1.read((char*)&b1,sizeof(b1)))
		{
			if(b1.get_rating()==5)
			{
			    cout<<setw(15)<<b1.get_dishname()<<"(*****)"<<setw(15)<<b1.get_cost()<<setw(20)<<b1.get_quantity();
			    cout<<endl;
			}
		    }
		    fin1.close();
		    fstream fin2("dish.dat", ios::binary | ios::in);
		    while(fin2.read((char*)&b1,sizeof(b1)))
		    {
			if(b1.get_rating()==4)
			{
			    cout<<setw(15)<<b1.get_dishname()<<"(****)"<<setw(16)<<b1.get_cost()<<setw(20)<<b1.get_quantity();
			    cout<<endl;
			}
		    }
		    fin2.close();
		    fstream fin3("dish.dat", ios::binary | ios::in);
		    while(fin3.read((char*)&b1,sizeof(b1)))
		    {
			if(b1.get_rating()==3)
			{
			    cout<<setw(15)<<b1.get_dishname()<<"(***)"<<setw(17)<<b1.get_cost()<<setw(20)<<b1.get_quantity();
			    cout<<endl;
			}
		    }
		    fin3.close();
		    fstream fin4("dish.dat", ios::binary | ios::in);
		    while(fin4.read((char*)&b1,sizeof(b1)))
		    {
			if(b1.get_rating()==2)
			{
			    cout<<setw(15)<<b1.get_dishname()<<"(**)"<<setw(18)<<b1.get_cost()<<setw(20)<<b1.get_quantity();
			    cout<<endl;
			}
		    }
		    fin4.close();
		    fstream fin5("dish.dat", ios::binary | ios::in);

		    while(fin5.read((char*)&b1,sizeof(b1)))
		    {
			if(b1.get_rating()==1)
			{
			    cout<<setw(15)<<b1.get_dishname()<<"(*)"<<setw(19)<<b1.get_cost()<<setw(20)<<b1.get_quantity();
			    cout<<endl;
			}
		    }
		    fin5.close();
		    fstream fin6("dish.dat", ios::binary | ios::in);

		    while(fin6.read((char*)&b1,sizeof(b1)))
		    {
			if(b1.get_rating()==0)
			{
			    cout<<setw(15)<<b1.get_dishname()<<"(NA)"<<setw(18)<<b1.get_cost()<<setw(20)<<b1.get_quantity();
			    cout<<endl;
			}
		    }
		    fin6.close();
		    break;
	case 3:
	{
	int category_ch;
	int count_german=0;
	int count_indian=0;
	int count_jap=0;
	int count_ital=0;
	int count_other=0;
	cout<<"ENTER CATEGORY YOU WISH TO LOOK FOR: \n1.GERMAN \n2.INDIAN \n3.JAPANESE \n4.ITALIAN \n5.OTHER"<<endl;
	cin>>category_ch; //category_ch is a variable for storing user's choice
	switch(category_ch)
	{
		case 1:
		{
			cout<<"CATEGORY: GERMAN"<<endl;
			fstream dish_by_category("dish.dat",ios::binary | ios::in);
			if(!dish_by_category)
			{
				cout<<"ERROR IN DISPLAYING MENU."<<endl;
				break;
			}

			cout<<setw(20)<<"|DISH NAME  "<<setw(20)<<" |COST Rs.  "<<setw(20)<<" |QUANTITY  "<<setw(15)<<" |RATING   "<<endl;
			while(dish_by_category.read((char*)&b1,sizeof(b1)))
			{
				if(strcmpi(b1.get_category(),"GERMAN")==0)
				{
					cout<<setw(20)<<b1.get_dishname()<<setw(15)<<b1.get_cost()<<setw(20)<<b1.get_quantity();
					count_german++;
					if(b1.get_rating()==0)
					  cout<<setw(15)<<"NA";
					else
					{
						int stars=b1.get_rating();
						cout<<setw(15);
						for(int k=1;k<=stars;k++)
						cout<<"*";
					}
					cout<<endl;
				 }
			}
			if(count_german==0)
			{
				cout<<"NO GERMAN FOOD."<<endl;
			}
			dish_by_category.close();
			break;
	  }
	  case 2:
		{
			cout<<"CATEGORY:INDIAN"<<endl;
			fstream dish_by_category("dish.dat",ios::binary | ios::in);
			if(!dish_by_category)
			{
				cout<<"ERROR IN DISPLAYING MENU."<<endl;
				break;
			}

			cout<<setw(20)<<"|DISH NAME  "<<setw(20)<<" |COST Rs.  "<<setw(20)<<" |QUANTITY  "<<setw(15)<<" |RATING  "<<endl;
			while(dish_by_category.read((char*)&b1,sizeof(b1)))
			{
				if(strcmpi(b1.get_category(),"INDIAN")==0)
				{
					cout<<setw(20)<<b1.get_dishname()<<setw(15)<<b1.get_cost()<<setw(20)<<b1.get_quantity();
					count_indian++;
					if(b1.get_rating()==0)
						cout<<setw(15)<<"NA";
					else
					{
						int stars=b1.get_rating();
						cout<<setw(15);
						for(int k=1;k<=stars;k++)
						cout<<"*";
					}
					cout<<endl;
				  }
			}
			if(count_indian==0)
			{
				cout<<"NO INDIAN FOOD."<<endl;
			}
			dish_by_category.close();
			break;
	  }
	  case 3:
		{
			cout<<"CATEGORY: JAPANESE"<<endl;
			fstream dish_by_category("dish.dat",ios::binary | ios::in);
			if(!dish_by_category)
			{
				cout<<"ERROR IN DISPLAYING MENU."<<endl;
				break;
			}

			cout<<setw(20)<<"|DISH NAME  "<<setw(20)<<" |COST Rs.  "<<setw(20)<<" |QUANTITY  "<<setw(15)<<" |RATING "<<endl;
			while(dish_by_category.read((char*)&b1,sizeof(b1)))
			{
				if(strcmpi(b1.get_category(),"JAPANESE")==0)
				{
					cout<<setw(20)<<b1.get_dishname()<<setw(15)<<b1.get_cost()<<setw(20)<<b1.get_quantity();
					count_jap++;
					if(b1.get_rating()==0)
					cout<<setw(15)<<"NA";
					else
					{
						int stars=b1.get_rating();
						cout<<setw(15);
						for(int k=1;k<=stars;k++)
						cout<<"*";
					}
					cout<<endl;
				    }
			}
			if(count_jap==0)
			{
				cout<<"NO JAPANESE FOOD."<<endl;
			}
			dish_by_category.close();
			break;
	  }
	  case 4:
		{
			cout<<"CATEGORY: ITALIAN"<<endl;
			fstream dish_by_category("dish.dat",ios::binary | ios::in);
			if(!dish_by_category)
			{
				cout<<"ERROR IN MENU."<<endl;
				break;
			}

			cout<<setw(20)<<"|DISH NAME "<<setw(20)<<" |COST Rs.  "<<setw(20)<<" |QUANTITY  "<<setw(15)<<" | RATING "<<endl;
			while(dish_by_category.read((char*)&b1,sizeof(b1)))
			{
				if(strcmpi(b1.get_category(),"ITALIAN")==0)
				{
					cout<<setw(20)<<b1.get_dishname()<<setw(15)<<b1.get_cost()<<setw(20)<<b1.get_quantity();
					count_ital++;
					if(b1.get_rating()==0)
					cout<<setw(15)<<"NA";
					else
					{
						int stars=b1.get_rating();
						cout<<setw(15);
						for(int k=1;k<=stars;k++)
						cout<<"*";
					}
					cout<<endl;

				}
			}
			if(count_ital==0)
			{
				cout<<"NO ITALIAN FOOD."<<endl;
			}
			dish_by_category.close();
			break;
	  }
	  case 5:
		{
			cout<<"CATEGORY: OTHER"<<endl;
			fstream dish_by_category("dish.dat",ios::binary | ios::in);
			if(!dish_by_category)
			{
				cout<<"ERROR IN DISPLAYING MENU."<<endl;
				break;
			}

			cout<<setw(20)<<"|DISH NAME "<<setw(20)<<" |COST Rs.  "<<setw(20)<<" |QUANTITY "<<setw(15)<<" |RATING "<<endl;
			while(dish_by_category.read((char*)&b1,sizeof(b1)))
			{
				if(strcmpi(b1.get_category(),"OTHER")==0)
				{
					cout<<setw(15)<<b1.get_dishname()<<setw(20)<<b1.get_cost()<<setw(20)<<b1.get_quantity();
					count_other++;
					if(b1.get_rating()==0)
					cout<<setw(15)<<"NA";
					else
					{
						int stars=b1.get_rating();
						cout<<setw(15);
						for(int k=1;k<=stars;k++)
						cout<<"*";
					}
					cout<<endl;
			       }
			}
			if(count_other==0)
			{
				cout<<"NO OTHER DISHES."<<endl;
			}
			dish_by_category.close();
			break;
	  }
	  default:
	  cout<<"THIS CATEGORY DOES NOT EXIST."<<endl;
	 }
	 break;
	 default:
	 cout<<"WRONG CATEGORY."<<endl;
	}
     }
}
void modify()
{
	clrscr();
	heading();
	cout<<endl;
	cout<<"MODIFY DISH"<<endl;
	display_dish();
    char name[50];//dish name to be modified
    dish tempDish;
    int flag = 0,founddish=0;
    fstream fin1("dish.dat",ios::binary|ios::in);
    fstream fout("temp.dat",ios::binary|ios::out);
    if(!fin1||!fout) {
	cout<<"THERE ARE NO DISHES TO BE MODIFIED."<<endl;
	return;
    }
    cout<<"ENTER THE NAME OF THE DISH YOU WANT TO MODIFY"<<endl;
    gets(name);
    while(fin1.read((char*)&tempDish,sizeof(tempDish)))
    {
	if(strcmpi(tempDish.get_dishname(), name)==0)
	{
		founddish=1;
	    do {
		cout<<"MODIFY MENU "<<endl;
		cout<<"1.COST"<<endl;
		cout<<"2.QUANTITY"<<endl;
		cout<<"3.DISH NAME"<<endl;
		cout<<"4.BACK TO PREVIOUS MENU"<<endl;
		char ch;
		cout<<"ENTER CHOICE"<<endl;
		cin>>ch;
		switch(ch)
		{
		    case '1':     tempDish.set_cost();
				break;
		    case '2':     tempDish.set_quantity();
				break;
		    case '3':	  tempDish.set_name();
				break;
		    case '4':     flag++;
				break;
		    default:    cout<<"WRONG CHOICE"<<endl;
		}
	    } while(flag==0);
	}
	fout.write((char*)&tempDish,sizeof(tempDish));
    }
    if(!founddish)
    {
	cout<<"DISH NOT FOUND"<<endl;
    }
    fin1.close();
    fout.close();
    remove("dish.dat");
    rename("temp.dat","dish.dat");
} //end of modify()   */

void view_rating()
{ //admin function
    char dishname[50];
    cout<<"ENTER THE NAME OF THE DISH YOU WANT TO VIEW RATING ABOUT"<<endl;
    gets(dishname);
    fstream fin1("dish.dat",ios::binary|ios::in);
    if(!fin1)
    {
	cout<<"THERE ARE NO DISHES TO VIEW THE RATINGS OF"<<endl;
	return;
    }
    int founddish=0;
    while(fin1.read((char*)&b1,sizeof(b1)))
    {
	if(strcmp(b1.get_dishname(),dishname)==0)
	{
	 if(b1.get_rating()==0)
	 {
		cout<<"DISH HAS NOT YET BEEN RATED"<<endl;
	 }
	 else
	 {
		cout<<"THE RATING OF THE DISH IS : "<<b1.get_rating()<<" OUT OF  5 "<<endl;
	 }
	 founddish=1;
	}
    }
    if(!founddish)
    {
	cout<<"DISH NOT FOUND"<<endl;
    }

    fin1.close();
}

void decrease_dish_quantity(cart_item item)
{
    fstream fin("dish.dat",ios::binary|ios::in|ios::out);
    if(!fin)
    {
	cout<<"ERROR!"<<endl;
	return;
    }
    while(fin.read((char*)&b1,sizeof(b1)))
    {
	if(strcmp(b1.get_dishname(),item.dishname)==0)
	{
	    int temp_qty = b1.get_quantity() - (item.quantity);
	    b1.set_quantity(temp_qty);
	}
	fin.seekp(fin.tellp()-1*sizeof(b1));
	fin.write((char*)&b1,sizeof(b1));
    }
}

void buy_dish()
{
	clrscr();
	heading();
    if(user1.get_cart_items()==10)
    {
	cout<<"CART FULL!\n";
	return;
    }
    char searched_dish[100];
    int req_quantity;
    int flag = -1; //for searching dish
    char choice1;
    cout<<"\t\t\t\t\"BUY FOOD\""<<endl;
    display_dish();
    cout<<endl;
    cout<<"\nWHICH DISH ARE YOU LOOKING FOR?"<<endl;
    gets(searched_dish);
    fstream fin1("dish.dat", ios::in | ios::binary);
    if(!fin1) {
	cout<<"ERROR IN OPENING FILE."<<endl;
    }
    while(fin1.read((char*)&b1,sizeof(b1)))
     {
	if((strcmp(b1.get_dishname(),searched_dish)) == 0 && b1.get_quantity() > 0)
	{
	    flag = 1;
	    cout<<searched_dish<<" IS IN STORE"<<endl;
	    cout<<"DETAILS OF THE DISH: "<<endl;
	    b1.display();
	    if(b1.get_quantity() < 5)
	    {
		cout<<"\n\tBUY SOON!."<<endl;
	    }
	    cout<<"TO BUY THIS DISH, PRESS Y"<<endl;
	    cin>>choice1;
	    if(choice1 == 'y' || choice1 == 'Y')
	    {
	       for(int i=0;i<loggedin_user.get_items();i++)
		{
			if(strcmp(loggedin_user.get_cart(i).dishname,searched_dish)==0)
			{
			    cout<<"DISH ALREADY IN CART!"<<endl;
			    return;
			}
		}
		strcpy(item.dishname,searched_dish);
		int req_quantity;
		do {
		    cout<<"ENTER QUANTITY:"<<endl;
		    cin>>req_quantity;
		    if(b1.get_quantity()<req_quantity)
			cout<<"ENTERED QUANTITY IS GREATER THAN THE CURRENT AVAILABLE STOCK"<<endl<<"TRY AGAIN."<<endl;
		    else
		    {   dish o1;
			fstream fin("dish.dat",ios::binary|ios::in);
			fstream fout("D.dat",ios::binary|ios::out|ios::app);
			if(!fout||!fin)
			   {
				cout<<"MENU NOT WORKING. PLEASE TRY TO ADD ITEMS LATER.";
				return;
			   }
			   while(fin.read((char*)&o1,sizeof(o1)))
			    {
				if(strcmp(o1.get_dishname(),searched_dish)==0)
				{
					o1.newquantity("cart_add",req_quantity);
					fout.write((char *)&o1,sizeof(o1));
				}
				else
				fout.write((char*)&o1,sizeof(o1));
			    }
			    fin.close();
			    fout.close();
			    remove("dish.dat");
			    rename("D.dat","dish.dat");
		    }
		} while(b1.get_quantity()<req_quantity || req_quantity<=0);
		item.quantity=req_quantity;
		item.cost=b1.get_cost();
		//b1.decrease_quantity(item);
		add_to_cart(); //passes the dish to the cart
	    }
	    else
		return;
	}
	else if(b1.get_quantity()==0 && flag ==0)
	{
		cout<<"WE'RE SORRY! FOOD OUT OF STOCK"<<endl;
		flag=0;
	}
    }
    clrscr();
    if(flag == -1)
    {
	cout<<"DISH NOT FOUND\n";
    }
    fin1.close();

    cout<<"\nWANT TO SEARCH FOR ANOTHER DISH? \nPRESS 'Y' TO CONTINUE OR PRESS 'N' TO LEAVE."<<endl;
    char choice2;
    label:
    cin>>choice2;
    if(choice2 == 'Y' || choice2 == 'y')
    {
	buy_dish();
    }
    else if(choice2 == 'N' || choice2 =='n')
    {
	return;
    }
    else
    {
	cout<<"\tWRONG CHOICE"<<endl;
	cout<<"PLEASE ENTER AGAIN!"<<endl;
	goto label;
    }
    //fin1.close();
}

void heading()
{
	textbackground(BLACK);

	clrscr();
	{

		{
			textbackground(BLACK);
			textcolor(CYAN+BLINK);
			cprintf("================================================================================");
		}
		{
			textcolor(LIGHTGRAY);
			cprintf("                                   FOOD INC.                                    ");
		}
		{
			textcolor(CYAN+BLINK);
			cprintf("================================================================================");
		}

	}
		cout<<endl;
		textcolor(LIGHTGRAY);

}

depart()
{
		clrscr();
		{
			textbackground(BLACK);
			textcolor(CYAN+BLINK);
			cprintf("================================================================================");
		}
		{
			textcolor(LIGHTGRAY);
			cprintf("                                   FOOD INC.                                    ");
		}
		{
			textcolor(CYAN+BLINK);
			cprintf("================================================================================");
		}
		cout<<endl;
		cout<<endl<<setw(42)<<" CREDITS";

	       /*
	       cout<<endl<<setw(42);
	       {
			textcolor(CYAN+BLINK);
			cprintf(" CREDITS");
	       }
	       */

		cout<<endl<<endl<<endl<<endl;

	       // textcolor(LIGHTGRAY);

		cout<<setw(48)<<"THANK YOU UZMA MA'AM";
		cout<<endl<<endl;
		cout<<endl<<setw(45)<<"A PROGRAM BY";
		cout<<endl<<setw(46)<<"KUSHAL KRISHNA";
		cout<<endl<<setw(45)<<" ROSHAN ISMAIL";
		cout<<endl<<setw(45)<<" SAGAR MAHAJAN";
		cout<<endl<<setw(42)<<"  OF 12C";
		cout<<endl<<setw(42)<<" 2019-20";
		getch();
		//delay(5000);

}

void main()
{ //main function
    clrscr();
    char option; //for login


    loop:
    heading();

    cout<<"1.LOG IN"<<endl;
    cout<<"2.SIGN UP"<<endl;
    cout<<"3.EXIT"<<endl;

    cout<<"Enter Your Choice: ";
    cin>>option;

    switch(option)
    {
	case '1':
		login();
		break;

	case '2':
		signup();
		break;

	case '3':
		depart();
		exit(0);

	default:
		cout<<endl<<"OOPS. INVALID OPTION. TRY AGAIN"<<endl;
		getch();
		break;
    }

    getch();
    goto loop;
} //end of main



