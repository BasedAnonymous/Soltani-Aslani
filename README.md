//# Soltani-Aslani
//UT Project
#include <iostream>
#include <vector>
#include <string>
#include<ctime>

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

int months_length(std :: string input ){
    int result;

    if(input == "Jan")
        return result = 1;

    else if(input == "Feb")
        result = 2;

    else if(input == "Mar")
        result = 3;

    else if(input == "Apr")
        result = 4;

    else if(input == "May")
        result = 5;

    else if(input == "Jun")
         result = 6;

    else if(input == "Jul")
        result = 7;

    else if(input == "Aug")
        result = 8;

    else if(input == "Sep")
        result = 9;

    else if(input == "Oct")
        result = 10;

    else if(input == "Nov")
        result = 11;

    else if(input == "Dec")
        result = 12;

    return result;
}

std :: string add_date(){
    std :: time_t my_time = time(0);
    std :: string time = ("%s", ctime(&my_time));
    time.pop_back();
    return time;

}

std :: string delay_count(std :: string member_name , int which_book) {

    struct data {
        int day;
        int hour;
        int minute;
        int second;
        std :: string month;
        int year;
        std :: string help;
    };

    std :: ifstream file_search;
    std :: string lines;
    std :: vector<std :: string>tempo;
    int count{0} , que;
    file_search.open("Persons.txt");

    while(getline(file_search,lines)){
        if(cutter(lines,1)==member_name)
            que = count;
        tempo.push_back(lines);
        count++;
    }
    file_search.close();

    std :: string input_1 =cutter(tempo[que] , 12 + which_book);
    std :: time_t my_time = time(0);
    std :: string input_2 = ("%s", ctime(&my_time));
    data sample_1 , sample_2;


    sample_1.year =  stoi(input_1.substr(20,4));
    sample_1.month =  (input_1.substr(4,3));
    sample_1.day =  stoi(input_1.substr(8,2));
    sample_1.hour = stoi(input_1.substr(11,2));
    sample_1.minute = stoi(input_1.substr(14,2));

    sample_2.year =  stoi(input_2.substr(20,4));
    sample_2.month =  (input_2.substr(4,3));
    sample_2.day =  stoi(input_2.substr(8,2));
    sample_2.hour = stoi(input_2.substr(11,2));
    sample_2.minute = stoi(input_2.substr(14,2));
    sample_2.help = input_2.substr(4,3);

    int result_min = sample_2.minute - sample_1.minute;
    int result_h = sample_2.hour - sample_1.hour;
    int result_day = sample_2.day - sample_1.day;
    int result_month = months_length(sample_2.month) - months_length(sample_1.month);
    int result_year = sample_2.year - sample_1.year;

    if (result_min < 0){
        result_h--;
        result_min += 60;
    }


    if (result_h < 0){
        result_day--;
        result_h+= 24;
    }

    if (result_day < 0){  
        result_month--;
        result_day += 30;
    }

    if (result_month < 0){
        result_year--;
        result_month += 12;
    }
    
    if(result_year == 0 && result_month == 0 && result_day*24*60+result_h*60+result_min <= 2880)
        return "on time";

    else {
        std :: string delay_time = "you are late by " + std :: to_string(result_year) + " year(s) and "
        + std :: to_string(result_month) + " month(s) and " + std :: to_string(result_day) + " day(s) and "
        + std :: to_string(result_h) + " hours and " + std :: to_string(result_min) + " minutes.";

        return delay_time;
    }

}

void goodbye(std :: string user_name , std :: string file_name){

    std :: fstream reading_file;
    std :: vector<std :: string> help;
    reading_file.open(file_name);
    int finding{0};
    std :: string line;
    int suspect;


    while(getline(reading_file,line)){
        help.push_back(line);
        finding++;

        if(cutter(line,1)==user_name){
            suspect = finding;
        }
        
    }
    reading_file.close();


    int size = help.size();
    std :: ofstream writing_file;
    writing_file.open(file_name);
    for(int count = 0 ; count < size ; count ++){

        if(count != suspect-1)
            writing_file << help[count] << std :: endl;
            
    }

    writing_file.close();
}


void goodbye_book(std :: string isbn , std :: string file_name){

    std :: fstream reading_file;
    std :: vector<std :: string> help;
    reading_file.open(file_name);
    int finding{0};
    std :: string line;
    int suspect;


    while(getline(reading_file,line)){
        help.push_back(line);
        finding++;

        if(cutter(line,5)==isbn){
            suspect = finding;
        }
        
    }
    reading_file.close();

    std :: ofstream writing_file;
    int size = help.size();
    writing_file.open(file_name);
    for(int count = 0 ; count < size ; count ++){

        if(count != suspect-1)
            writing_file << help[count] << std :: endl;
            
    }
    writing_file.close();

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
