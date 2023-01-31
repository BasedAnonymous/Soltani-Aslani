//# Soltani-Aslani
//UT Project
#include <iostream>
#include <vector>
#include <string>

#include <fstream>
using namespace std;



string cutter(string a , int b){
    vector<int> ignors;
    int v = 0;
    for(int i = 0 ; i < a.size() ; i++){
        if(a[i] == '_'){
            ignors.push_back(i);
            v++;
        
    }
}
int enteha = ignors[b] - ignors[b - 1] - 1;
return a.substr(ignors[b - 1] + 1 ,enteha );


}






class Book{
    
    private :
    
    string title;
    string authors;
    string publisher_Name;
    string subjects;
    string borrower_User_Name = "free";
    
    
    int ISBN;
    int shelf_Number;
    int published_Year;
    int number_Of_Pages;
    int edition;
    int number_Of_Used;
    
    
    
    public :
    
    friend string Borrowing(string string_search_borrowing);
    friend string Borrowing(int int_search_borrowing);
    
    friend string Return(string string_search_return);
    friend string Return(int int_search_return);
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
};







class Person{
    
   private :
   
   string user_Name;
   string password;
   string first_Name;
   string last_Name;
   struct Birth_Date{
       int year;
       int month;
       int day;
   };
   Birth_Date birth_Date;
   string is_Root_User = "No";
   int borrowed = 0;
   string book1 = "free";
   string book2 = "free";
   int members;
   int is_Member = 0;
   
   
   
   public :
   
   void login(string user_Name , string password){
      if(is_Member == 0){
       
       ifstream read("Persons.txt");
       
       string person;
       while(getline(read , person)){
           
           
           if(user_Name == cutter(person,1) && password == cutter(person,2)){
               
               is_Member++;
               read.close();
               break;
           }
       }
       
       
       if(is_Member == 1){
           this->user_Name = cutter(person,1);
           this->password = cutter(person,2);
           first_Name = cutter(person,3);
           last_Name = cutter(person,4);
           birth_Date = { stoi(cutter(person,5)) , stoi(cutter(person,6)) , stoi(cutter(person,7))};
           is_Root_User = cutter(person,8);
           borrowed = stoi(cutter(person,9));
           book1 = cutter(person,10);
           book2 = cutter(person,11);
           cout << " Hello " <<  this->first_Name <<" " << this->last_Name;
           cout << "\n Welcome to the library.\n\n";
           
           
       
   }else{
       cout << " Sorry, you are not registered";
       cout << "\n or input is wrong.\n";
   }
      }else{
          cout << "\n You have already entered.\n";
      }
   }
   
   void sign_Up(string user_Name , string password , string first_Name , string last_Name , Birth_Date birth_Date){
       if(is_Member == 1){
           cout << " You are registered before\n";
           cout << " You have already entered.\n";
   }else{
       ifstream read1("Persons.txt");
       string person1;
       int error = 0;
       while(getline(read1 , person1)){
       if(first_Name == cutter(person1,3) && last_Name == cutter(person1,4)){
               cout << "\n You are registered before\n";
               cout << " Please login first.\n";
               error++;
           }
           else if(user_Name == cutter(person1,1)){
               cout <<"\n This user name already exists";
               cout << "\n Please use another username :\n\n";
               string new_Username;
               cout << " Different user name : ";
               cin >> new_Username;
               user_Name = new_Username;
               
               break;
                                
           }
       }
       read1.close();
       if(error == 0){
               ofstream write;
               write.open("Persons.txt",ofstream::app);
               write << "_" << user_Name << "_" << password << "_" << first_Name << "_" << last_Name << "_" 
               << birth_Date.year << "_" << birth_Date.month << "_" << birth_Date.day << "_" << "No" << "_" 
               << "0" << "_" << "free" << "_" << "free" << "_" << "\n";
               write.close();
               this->user_Name = user_Name;
               this->password = password;
               this->first_Name = first_Name;
               this->last_Name = last_Name;
               this->birth_Date = {birth_Date.year , birth_Date.month , birth_Date.day};
               is_Member++;
               cout << " Welcome " << this->first_Name << " " << this->last_Name ;
               cout << "\n* Your registration was successfully completed *\n";
               cout << " now you logged in.\n";
       }
       
   }
   }
   
   
   
   
   string Search(string string_search){
       if(is_Member == 1){
       int number_Of_Exist_Books = 0;
       ifstream read_Search_string("Books.txt");
       string book_Line;
       vector<string> exist_books_list;
       while(getline(read_Search_string ,book_Line)){
           for(int g = 1 ; g <= 4 ; g++){
               if(cutter(book_Line,g) == string_search){
                   number_Of_Exist_Books++;
                   exist_books_list.push_back(book_Line);
                   break;
               }
           }
       }
       read_Search_string.close();
       if(number_Of_Exist_Books == 1){
           string khorooji;
           for(int a = 1 ; a <= 11 ; a++){
                   if(a != 5){
                       if(a != 11){
                       khorooji += cutter(exist_books_list[0],a) + "  ";
                       }else{
                           khorooji += cutter(exist_books_list[0],a) ;
                       }
                   }
               }
               return khorooji;
           
       }else if(number_Of_Exist_Books == 0){
           return "\n Sorry, We don't have any book with this characteristic.\n";
       }else{
           string khorooji[number_Of_Exist_Books];
           for(int b = 0 ; b < number_Of_Exist_Books ; b++){
               
               for(int a = 1 ; a <= 11 ; a++){
                   if(a != 5){
                       if(a != 11){
                       khorooji[b] += cutter(exist_books_list[b],a) + "  ";
                       }else{
                           khorooji[b] += cutter(exist_books_list[b],a) ;
                       }
                       
                   }
               }
               
           }
           for(int u = 0 ; u < number_Of_Exist_Books ; u++){
               cout << u + 1 <<" - "<<khorooji[u];
               
           }
           cout << "\n Please choose one of this books :\n";
           int select;
           cin >> select ;
           if(select != 0){
           return khorooji[select - 1];
           }else{
               return "\n Thanks, the search finished\n";
           }
       }
       
       
       
       }else{
          return "\n Please login or sign up first.\n"; 
       }   
   }
   
   
   
   
   
 
   string Search(int int_search){
       
       if(is_Member == 1){
       int number_Of_Exist_Books = 0;
       ifstream read_Search_int("Books.txt");
       string book_Line;
       vector<string> exist_books_list;
       while(getline(read_Search_int ,book_Line)){
           for(int g = 6 ; g <= 10 ; g++){
               if(stoi(cutter(book_Line,g)) == int_search){
                   number_Of_Exist_Books++;
                   exist_books_list.push_back(book_Line);
                   break;
               }
           }
       }
       read_Search_int.close();
       if(number_Of_Exist_Books == 1){
           string khorooji;
           for(int a = 1 ; a <= 11 ; a++){
                   if(a != 5){
                       if(a != 11){
                       khorooji += cutter(exist_books_list[0],a) + "  ";
                       }else{
                           khorooji += cutter(exist_books_list[0],a) ;
                       }
                   }
               }
               return khorooji;
           
       }else if(number_Of_Exist_Books == 0){
           return "\n Sorry, We don't have any book with this characteristic.\n";
       }else{
           string khorooji[number_Of_Exist_Books];
           for(int b = 0 ; b < number_Of_Exist_Books ; b++){
               
               for(int a = 1 ; a <= 11 ; a++){
                   if(a != 5){
                       if(a != 11){
                       khorooji[b] += cutter(exist_books_list[b],a) + "  ";
                       }else{
                           khorooji[b] += cutter(exist_books_list[b],a) ;
                       }
                       
                   }
               }
               
           }
           for(int u = 0 ; u < number_Of_Exist_Books ; u++){
               cout << u + 1 <<" - "<<khorooji[u];
               
           }
           cout << "\n Please choose one of this books :\n";
           int select;
           cin >> select ;
           if(select != 0){
           return khorooji[select - 1];
           }else{
               return "\n Thanks, the search finished\n";
           }
       }
       
       
       
       }else{
          return "\n Please login or sign up first.\n"; 
       } 
   }
   
   
   
   
  
   
   string Borrowing(string string_search_borrowing){
       if(is_Member == 1){
           
       if(Search(string_search_borrowing) != "\n Sorry, We don't have any book with this characteristic.\n"
       || Search(string_search_borrowing) != "\n Thanks, the search finished\n"){
       if(borrowed < 2){
       borrowed++;
       ofstream borrow_string("Persons.txt");
       
       }else{
           return "\n Sorry, you can't borrow more than 2 books.\n";
       
       }
       }
       else{
           
       }
       }else{
           return "\n Please login or sign up first.\n";
       }
       } 
   
   
   /*
   string Borrowing(int int_search_borrowing){
       
   }
   
   string Return(string string_search_return){
       
   }
   string Return(int int_search_return){
       
   }
    */
};













int main(){

    Person p1;
    int first_Step;
    cout << "\n Hello, Please login or sign up first.\n";
    cout << " 1 : login\t2 : sign up\t3 : exit\n\n ";
    cin >> first_Step;
    if(first_Step == 1){
        string id;
        string ramz;
        cout << " Username : ";
        cin >> id;
        cout << " Password : ";
        cin >> ramz;
        p1.login(id,ramz);
    }else if(first_Step == 2){
        string esm;
        string famili;
        string idd;
        string ramzz;
        int sal;
        int mah; 
        int rooz;
        cout << " First name : ";
        cin >> esm;
        cout << " Last name : ";
        cin >> famili;
        cout << " Username : ";
        cin >> idd;
        cout << " Password : ";
        cin >> ramzz;
        cout << " Year of birth date : ";
        cin >> sal;
        cout << " Month of birth date : ";
        cin >> mah;
        cout << " Day of birth date : ";
        cin >> rooz;
        p1.sign_Up(idd,ramzz,esm,famili,{sal,mah,rooz});
    }else if (first_Step == 3){
        
        cout << "\n\n Hope to see you again.";
        
    }
    /*
    if(p1.is_Member == 1 && p1.is_Root_User == "Yes"){
        cout << "\n You are Root user\n";
        cout << " 1 : Search\t2 : borrow\t3 : Return\t4:";
    }
    
    */
    
    
    
    




    return 0;
}
