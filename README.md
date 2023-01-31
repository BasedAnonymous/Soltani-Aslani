//# Soltani-Aslani
//UT Project
#include <iostream>
#include <vector>
#include <string>
#include <ctime>
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

std :: string add_time(){
    std :: time_t my_time = time(0);
    std :: string time = ("%s", ctime(&my_time));
    time.pop_back();
    return time;
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




void CHANGER_book(std :: string ISBN , int cutter_cut , std :: string aim_variable){
    std :: vector <std :: string> holder;
    std :: ifstream file_search;
    std :: string lines;
    file_search.open("Books.txt");
    int order{0} , aim;

    while(getline(file_search,lines)){
        holder.push_back(lines);
        if(cutter(holder[order],5) == ISBN)
            aim = order;
        order++;
    }
    file_search.close();


    std :: ofstream file_retype;
    file_retype.open("Books.txt");
    for(int count = 0 ; count < holder.size() ; count++){
        if(count != aim)
            file_retype << holder[count] << std :: endl;
        else if(count == aim){
            std :: string help="_";
            for(int counter{1} ; counter <= 11 ; counter++){
                if(counter != cutter_cut)
                    help += cutter(holder[aim],counter) + "_";
                else if(counter == cutter_cut)
                    help += aim_variable + "_";
            }
            file_retype << help << std :: endl;
        }
    }
    file_retype.close();

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
   int the_Number_Of_Delays = 0;
   string time_Book1 = "free";
   string time_Book2 = "free";
   int extension_Book1 = 0;
   int extension_Book2 = 0;
   


   int is_Member = 0;
   
   
   
   public :



   string get_user_Name(){
    return user_Name;
   }
   string get_password(){
    return password;
   }
   string get_first_Name(){
    return first_Name;
   }
   string get_last_Name(){
    return last_Name;
   }
   Birth_Date get_birth_Date(){
    return birth_Date;
   }
   string get_is_Root_User(){
    return is_Root_User;
   }
   int get_borrowed(){
    return borrowed;
   }
   string get_book1(){
    return book1;
   }
   string get_book2(){
    return book2;
   }
   int get_the_Number_Of_Delays(){
    return the_Number_Of_Delays;
   }
   string get_time_Book1(){
    return time_Book1;
   }
   string get_time_Book2(){
    return time_Book2;
   }
   int get_extension_Book1(){
    return extension_Book1;
   }
   int get_extension_Book2(){
    return extension_Book2;
   }
   int get_is_Member(){
       return is_Member;
   }
   void set_is_Member(int is_Member){
       this->is_Member = is_Member;
   }
   


   Person(){
    user_Name = "None";
    password = "None";
    first_Name = "None";
    last_Name = "None";
    birth_Date = {1,1,1};
    is_Root_User = "No";
    borrowed = 0;
    book1 = "free";
    book2 = "free";
    the_Number_Of_Delays = 0;
    time_Book1 = "free";
    time_Book2 = "free";
    extension_Book1 = 0;
    extension_Book2 = 0;

    is_Member = 0;
   }
   
   void login(string user_Name , string password){
      if(is_Member == 0){
       
       ifstream read("Persons.txt");
       
       string person;
       while(getline(read , person)){
           
           
           if(user_Name == cutter(person,1) && password == cutter(person,2)){
               if(stoi(cutter(person,12)) > 2){
                 cout << " Something went wrong.\n Your account is suspended.";
                 cout << "\n You have not returned the borrowed books in time more than twice.\n";
                 read.close();
                 break;
               }else{
               is_Member++;
               read.close();
               break;
               }
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
           the_Number_Of_Delays = stoi(cutter(person,12));
           time_Book1 = cutter(person,13);
           time_Book2 = cutter(person,14);
           extension_Book1 = stoi(cutter(person,15));
           extension_Book2 = stoi(cutter(person,16));


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

   

   
   void sign_Up(string user_Name , string password , string first_Name , string last_Name , Birth_Date birth_Date , string append){
       if(is_Member == 1 && append == "No"){
           cout << " You are registered before\n";
           cout << " You have already entered.\n";
   }else{
       ifstream read1("Persons.txt");
       string person1;
       int error = 0;
       while(getline(read1 , person1)){
       if(first_Name == cutter(person1,3) && last_Name == cutter(person1,4)){
               cout << "\n The information of This person is registered before\n";
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
               fstream write;
               write.open("Persons.txt",ofstream::app);
               write << "_" << user_Name << "_" << password << "_" << first_Name << "_" << last_Name << "_" 
               << birth_Date.year << "_" << birth_Date.month << "_" << birth_Date.day << "_" << "No" << "_" 
               << "0" << "_" << "free" << "_" << "free" << "_" << "0" <<"_"<< "free"<<"_"<< "free"<<"_"<<"0"<<"_"
               << "0"<< "_"<<"\n";
               write.close();
               this->user_Name = user_Name;
               this->password = password;
               this->first_Name = first_Name;
               this->last_Name = last_Name;
               int correct_date = 0;
               if(birth_Date.year <= 1401 && birth_Date.year >= 0){
                   correct_date++;
               }else{
                   while(birth_Date.year > 1401 || birth_Date.year < 0){
                           int saljadid;
                           cout << "Wrong, please enter correct number for year :";
                           cin >> saljadid;
                           birth_Date.year = saljadid;
                   }
                  correct_date++; 
               }
               if(birth_Date.month <= 12 && birth_Date.month > 0){
                       correct_date++;
                   }else{
                      while(birth_Date.month > 12 || birth_Date.month <= 0){
                           int mahjadid;
                           cout << "Wrong, please enter correct number for month :";
                           cin >> mahjadid;
                           birth_Date.month = mahjadid;
                           }
                           correct_date++;
                   }
                   if(birth_Date.day <= 31 && birth_Date.day > 0){
                           correct_date++;
                       }else{
                           while(birth_Date.day > 31 || birth_Date.day <= 0){
                           int roozjadid;
                           cout << "Wrong, please enter correct number for day :";
                           cin >> roozjadid;
                           birth_Date.day = roozjadid;
                           }
                           correct_date++;
                       }
                       if(correct_date == 3){
                           this->birth_Date = {birth_Date.year , birth_Date.month , birth_Date.day};
                       }
               
               is_Member++;
               cout << "\n * " << this->first_Name << " " << this->last_Name;
               cout << "'s registration has been successfully completed *\n";
              
       }
       
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
               fstream write;
               write.open("Persons.txt",ofstream::app);
               write << "_" << user_Name << "_" << password << "_" << first_Name << "_" << last_Name << "_" 
               << birth_Date.year << "_" << birth_Date.month << "_" << birth_Date.day << "_" << "No" << "_" 
               << "0" << "_" << "free" << "_" << "free" << "_" << "0" <<"_"<< "free"<<"_"<< "free"<<"_"<<"0"<<"_"
               << "0"<< "_"<<"\n";
               write.close();
               this->user_Name = user_Name;
               this->password = password;
               this->first_Name = first_Name;
               this->last_Name = last_Name;
               int correct_date = 0;
               if(birth_Date.year <= 1401 && birth_Date.year >= 0){
                   correct_date++;
               }else{
                   while(birth_Date.year > 1401 || birth_Date.year < 0){
                           int saljadid;
                           cout << "Wrong, please enter correct number for year :";
                           cin >> saljadid;
                           birth_Date.year = saljadid;
                   }
                  correct_date++; 
               }
               if(birth_Date.month <= 12 && birth_Date.month > 0){
                       correct_date++;
                   }else{
                      while(birth_Date.month > 12 || birth_Date.month <= 0){
                           int mahjadid;
                           cout << "Wrong, please enter correct number for month :";
                           cin >> mahjadid;
                           birth_Date.month = mahjadid;
                           }
                           correct_date++;
                   }
                   if(birth_Date.day <= 31 && birth_Date.day > 0){
                           correct_date++;
                       }else{
                           while(birth_Date.day > 31 || birth_Date.day <= 0){
                           int roozjadid;
                           cout << "Wrong, please enter correct number for day :";
                           cin >> roozjadid;
                           birth_Date.day = roozjadid;
                           }
                           correct_date++;
                       }
                       if(correct_date == 3){
                           this->birth_Date = {birth_Date.year , birth_Date.month , birth_Date.day};
                       }
               
               is_Member++;
               cout << "\n Welcome " << this->first_Name << " " << this->last_Name;
               cout << "\n* Your registration was successfully completed *\n";
               cout << " now you logged in.\n";
       }
       
   }
   }
   
   
   
   std :: string globo_var;
   string Search(string string_search){
       
       
       if(is_Member == 1){
           
           
           
       int number_Of_Exist_Books = 0;
       ifstream read_Search_string("Books.txt");
       string book_Line;
       vector<string> exist_books_list;
       
       while(getline(read_Search_string ,book_Line)){
           for(int g = 1 ; g <= 10 ; g++){
            if((cutter(book_Line,g)).size() >= string_search.size()){
               for(int z = 0 ; z <= (cutter(book_Line,g)).size() - string_search.size() ; z++){
                if((cutter(book_Line,g)).substr(z,string_search.size()) == string_search){
                   globo_var=(cutter(book_Line,5));
                   number_Of_Exist_Books++;
                   exist_books_list.push_back(book_Line);
                   break;
                }
               }
           }
       }
       }
       
       
       
       
       
       read_Search_string.close();
       if(number_Of_Exist_Books == 1){
           string khorooji;
           for(int a = 1 ; a <= 11 ; a++){
               if(a == 11){
                       if(cutter(exist_books_list[0],11) == "free"){
                           khorooji += "_" + cutter(exist_books_list[0],a) + "_";
                       }else{
                           
                           khorooji += "_borrowed_";
                       }
               }else{
                  khorooji += "_" + cutter(exist_books_list[0],a) ; 
                       }
                       
               }
               
               
                       
          
          cout << " ### title | authors | pub_name | subjects |  ISBN  | shelf_num | pub_year | pages | edition | used | status ###\n";
          cout << khorooji + "\n";
          return khorooji + "\n";
                       
                   
               
               
           
       }else if(number_Of_Exist_Books == 0){
           return "\n Sorry, We don't have any book with this characteristic.\n";
       }else{



           string khorooji[number_Of_Exist_Books];
           for(int b = 0 ; b < number_Of_Exist_Books ; b++){
               
               for(int a = 1 ; a <= 11 ; a++){
                   if(a == 11){
                       if(cutter(exist_books_list[b],11) == "free"){
                           khorooji[b] += "_" + cutter(exist_books_list[b],a) + "_";
                       }else{
                           khorooji[b] += "_borrowed_";
                       }
                    }else{
                      khorooji[b] += "_" + cutter(exist_books_list[b],a); 
                       }
                 
                   }
               }
       
               
           cout << " ### title | authors | pub_name | subjects |  ISBN  | shelf_num | pub_year | pages | edition | used | status ###\n";
           for(int u = 0 ; u < number_Of_Exist_Books ; u++){
               cout << " "<< u + 1 <<" : "<<khorooji[u] << "\n";
               
           }
           cout << "\n Please choose one of this books : ";
           int select;
           cin >> select ;
           if(select != 0){
               
           return khorooji[select - 1];
           }
           else{
               return "\n Thanks, the search finished\n";
           }






       }  
       }else{
          return "\n Please login or sign up first.\n"; 
       }   
       
    
       
   }

   
   
   
   
   
   
 
   
   
   
   
  
   
   void Borrowing(string string_search_borrowing){
       if(is_Member == 1){
       string book = Search(string_search_borrowing);   
       if(book != "\n Sorry, We don't have any book with this characteristic.\n"
       && book != "\n Thanks, the search finished\n"){
       if(cutter(book,11) == "free"){
       if(borrowed < 2){

       
       
       if(borrowed == 0){
        this->time_Book1 = add_time();
        borrowed++;
        this->book1 = (cutter(book,5));
        CHANGER_book(book1,11,this->user_Name);

        
        
        
        
       }else if(borrowed == 1){
        this->book2 = (cutter(book,5));
        this->time_Book2 = add_time();
        borrowed++;
        CHANGER_book(book2,11,this->user_Name);
        
        
        
       }
       
       }else{
           cout << "\n Sorry, you can't borrow more than 2 books.\n";
       }
       }else{
           cout << "\n Sorry, someone else has already borrowed this item.\n";
       }
       }
       else{
           cout << book;
       }
       }else{
           cout << "\n Please login or sign up first.\n";
       }
       
       } 
   
   



   
   
   void Return(){
       if(is_Member == 1){
       int wich;
       cout << "\n Wich of them you want to return ?\n";
       cout << "* Book 1 : ";
       cout << book1;
       cout << "\t* Book 2 : ";
       cout << book2 << "\n"; 
       cin >> wich;
       if(wich == 1){
        borrowed--;
        time_Book1 = "free";
        book1 = "free";
        cout << "\n Thank you for giving back the book on time.\n";
       }else if(wich == 2){
        borrowed--;
        time_Book2 = "free";
        book2 = "free";
        cout << "\n Thank you for giving back the book on time.\n";
       }
       }else{
          cout << "\n Please login or sign up first.\n";
       }
   }
   
    
};


void Menu(Person person2);



void First_Step(Person person){
    int first_Step;
    cout << " 1 : login\t2 : sign up\t3 : exit\n\n ";
    cin >> first_Step;
    if(first_Step == 1){
        string id;
        string ramz;
        cout << " Username : ";
        cin >> id;
        cout << " Password : ";
        cin >> ramz;
        person.login(id,ramz);
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
        person.sign_Up(idd,ramzz,esm,famili,{sal,mah,rooz});
    }else if (first_Step == 3){
        person.set_is_Member(0);
        cout << "\n\n Hope to see you again.";
        
    }
    if(person.get_is_Member() == 1 && person.get_is_Root_User() == "Yes"){
        cout << "\n You are Root user\n";
        Menu(person);
        
    }else if(person.get_is_Member() == 1 && person.get_is_Root_User() == "No"){
        Menu(person);
    }
}
    



void Update_Person(Person per);



          void Edit_Book(string editbook , Person person3){
          ifstream bookyab;
          bookyab.open("Books.txt");
          string khodeketab;
          while(getline(bookyab,khodeketab)){
            if(cutter(khodeketab,5) == editbook){
                break;
            }
          }
          int entekhabedit;
          cout << " Which characteristic you want to edit \n";
          cout << " 1 : Title\t2 : Authors\t3 : Publisher's name\t4 : Subjects\n";
          cout << " 5 : ISBN\t6 : Shelf number\t7 : Published year\t8 : Number of pages\n";
          cout << " 9 : Edition\t10 : Number of used\t11 : Borrower username\n";
          cin >> entekhabedit;
          string newvalue;
          cout << "\n Enter the new value : ";
          cin >> newvalue;
          string copy_book[11];
          for(int qw = 1 ; qw <= 11 ; qw++){
            if(qw != entekhabedit){
            copy_book[qw - 1] = cutter(khodeketab,qw);
            }else{
                copy_book[qw - 1] = newvalue;
            }
          }
          goodbye_book(cutter(khodeketab,5),"Books.txt");
          ofstream editedbook;
          editedbook.open("Books.txt",ofstream::app);
          for(int lm = 1 ; lm <= 11 ; lm++){
              editedbook << "_" << copy_book[lm - 1];
          }editedbook << "_" << "\n";
          
          editedbook.close();
          cout << "\n Editing the book has been done.\n";
          int moreedit;
          cout << "\n Do You want to edit this book again ?\n";
          cout << " 1 : Yes\t2 : No\n";
          cin >> moreedit;
          if(moreedit == 1){
                   Edit_Book(copy_book[4],person3); 
          }else{
               int newwork12;
                cout << " Do you have another work?\n 1 : Yes\t2 : No\n";
                cin >> newwork12;
                if(newwork12 == 1){
                    Menu(person3);

                }else if(newwork12 == 2){
        Update_Person(person3);
        person3.set_is_Member(0);
        cout << "\n Now you logged out.\n";
        First_Step(person3);
          }

          }
                }




                void Edit_User(string user_Name , Person person4){
                    ifstream useryab;
                    useryab.open("Persons.txt");
                    string khodetaraf;
                    while(getline(useryab,khodetaraf)){
                        if(cutter(khodetaraf,1) == user_Name){
                            break;
                        }
                    }
                    int entekhabeediteuser;
                    cout << " Which characteristic you want to edit \n";
                    cout << " 1 : Username\t2 : Password\t3 : First name\t4 : Last name\n";
                    cout << " 5 : Year of birth date\t6 : month of birth date\t7 : day of birth date\n";
                    cout << " 8 : Is root user\t9 : Borrowed\t10 : ISBN of book_1\t10 : ISBN of book_2\n";
                    cout << " 11 : The number of delays\t12 : The deadline for the first book\t13 : The deadline for the second book\n";
                    cin >> entekhabeediteuser;
                    string newpersonvalue;
                    cout << "\n Enter the new value : ";
                    cin >> newpersonvalue;
                    string copy_person[13];
                    for(int pw = 1 ; pw <= 13 ; pw++){
                       if(pw != entekhabeediteuser){
                          copy_person[pw - 1] = cutter(khodetaraf,pw);
                       }else{
                          copy_person[pw - 1] = newpersonvalue;
                       }
                    }
                    goodbye(user_Name,"Persons.txt");
                    ofstream updateperson;
                    updateperson.open("Persons.txt",ofstream::app);
                    for(int pu = 1 ; pu <= 13 ; pu++){
                        updateperson << "_" << copy_person[pu - 1];
                    }updateperson << "_" << "\n";
                    updateperson.close();
                    int moreeditperson;
                    cout << "\n Editing the person information has been done.\n";
                    cout << "\n Do You want to edit the information of this person again ?\n";
                    cout << " 1 : Yes\t2 : No\n";
                    cin >> moreeditperson;
                    if(moreeditperson == 1){
                        Edit_User(copy_person[0],person4);
                    }else{
                       int newwork14;
                       cout << " Do you have another work?\n 1 : Yes\t2 : No\n";
                       cin >> newwork14;
                       if(newwork14 == 1){
                            Menu(person4);

                       }else if(newwork14 == 2){
                          Update_Person(person4);
                          person4.set_is_Member(0);
                          cout << "\n Now you logged out.\n";
                          First_Step(person4);
                       }

                    }
                }
                
                
                
                
                
                
                
                
                void Update_Person(Person per){
    string copy_username = per.get_user_Name();
        string copy_pass = per.get_password();
        string copy_first = per.get_first_Name();
        string copy_last = per.get_last_Name();
        int copy_year = per.get_birth_Date().year;
        int copy_month = per.get_birth_Date().month;
        int copy_day = per.get_birth_Date().day;
        string copy_root = per.get_is_Root_User();
        int copy_borrowed = per.get_borrowed();
        string copy_book1 = per.get_book1();
        string copy_book2 = per.get_book2();
        int copy_The_number_of_delays = per.get_the_Number_Of_Delays();
        string copy_time1 = per.get_time_Book1();
        string copy_time2 = per.get_time_Book2();
        int copy_extension1 = per.get_extension_Book1();
        int copy_extension2 = per.get_extension_Book2();
        goodbye(per.get_user_Name(),"Persons.txt");
        ofstream updateperson;
        updateperson.open("Persons.txt",ofstream::app);
        updateperson << "_" << copy_username << "_" << copy_pass << "_" << copy_first << "_" << copy_last <<
        "_" << copy_year << "_" << copy_month << "_" << copy_day << "_" << copy_root << "_" << copy_borrowed <<
        "_" << copy_book1 << "_" << copy_book2 << "_" << copy_The_number_of_delays << "_" << copy_time1 << "_" <<
        copy_time2 << "_" << copy_extension1 << "_" << copy_extension2 << "_" << "\n";
        updateperson.close();
    
}














void Menu(Person person2){
cout << " 1 : Search\t2 : borrow\t3 : Extension\t4 : Return\t5 : Log-out\n";
if(person2.get_is_Root_User() == "Yes"){
        cout << " 6 : Append Book\t7 : Edit Book Information\t8 : Edit User Informations\n";
        cout << " 9 : Append User\t10 : Delete User\n ";
}
        int entekhab;
        cin >> entekhab;
        if(entekhab == 1){
           
                string search_string;
                cout << " Search item : ";
                cin >> search_string;
                person2.Search(search_string);
                int newwork;
                cout << " Do you have another work?\n 1 : Yes\t2 : No\n ";
                cin >> newwork;
                if(newwork == 1){
                    Menu(person2);

                }else if(newwork == 2){
                    
                    Update_Person(person2);
                    person2.set_is_Member(0);
        cout << "\n Now you logged out.\n";
        First_Step(person2);
        
                }
        }else if(entekhab == 2){
            string borrow_string;
            cout << "\n Item to borrow : ";
            cin >> borrow_string;
            person2.Borrowing(borrow_string);
            Update_Person(person2);
            int newwork;
                cout << " Do you have another work?\n 1 : Yes\t2 : No\n";
                cin >> newwork;
                if(newwork == 1){
                    Menu(person2);

                }else if(newwork == 2){
                    
                    person2.set_is_Member(0);
        cout << "\n Now you logged out.\n";
        First_Step(person2);
                }else if(entekhab == 3){
                    





                    
                }
            
    }else if(entekhab == 4){
        person2.Return();
        int newwork;
                cout << " Do you have another work?\n 1 : Yes\t2 : No\n";
                cin >> newwork;
                if(newwork == 1){
                    Menu(person2);

                }else if(newwork == 2){
                   Update_Person(person2);
                   person2.set_is_Member(0);
        cout << "\n Now you logged out.\n";
        First_Step(person2);
                }

    }else if(entekhab == 5){
        Update_Person(person2);
        Person();
        cout << "\n Now you logged out.\n";
        First_Step(person2);

    }
    if(person2.get_is_Root_User() == "Yes"){
      if(entekhab == 6){
        cout << "\n Enter the profile of the new book\n";
        string nameketab;
        cout << " Title : ";
        cin >> nameketab;
        string nevisandegan;
        cout << " Authors : ";
        cin >> nevisandegan;
        string entesharat;
        cout << " Publisher's name : ";
        cin >> entesharat;
        string mozooat;
        cout << " Subjects : ";
        cin >> mozooat;
        int aiesbien;
        cout << " ISBN : ";
        cin >> aiesbien;
        int shomareghafase;
        cout << " Shelf number : ";
        cin >> shomareghafase;
        int saleenteshar;
        cout << " Published year : ";
        cin >> saleenteshar;
        int tedadsafhe;
        cout << " Number of pages : ";
        cin >> tedadsafhe;
        int noskhe;
        cout << " Edition : ";
        cin >> noskhe;
        fstream bookenew;
        bookenew.open("Books.txt",ofstream::app);
        bookenew << "_" << nameketab << "_" << nevisandegan << "_" << entesharat << "_" << mozooat << "_" 
        << aiesbien << "_" << shomareghafase << "_" << saleenteshar << "_" << tedadsafhe << "_" << noskhe << "_" <<
        "0" << "_" << "free" << "_" << "\n";
        bookenew.close();
        cout << " The new book has been added.\n";
    }else if(entekhab == 7){
          string searchforeditbook;
          cout << "\n Search the book you want to edit its profile : ";
          cin >> searchforeditbook;
          string editbook = person2.Search(searchforeditbook);
          if(editbook != "\n Sorry, We don't have any book with this characteristic.\n"
            || editbook != "\n Thanks, the search finished\n"){
                    Edit_Book(cutter(editbook,5),person2);
            }else{
                cout << editbook;
                int newwork;
                cout << " Do you have another work?\n 1 : Yes\t2 : No\n";
                cin >> newwork;
                if(newwork == 1){
                    Menu(person2);

                }else if(newwork == 2){
                Person();
                cout << "\n Now you logged out.\n";
                First_Step(person2);
                }
            }
    }else if(entekhab == 8){
        string searchforeditperson;
        cout << "\n Enter the username of person you want to edit its profile : ";
        cin >> searchforeditperson;
        Edit_User(searchforeditperson,person2);
        
          

    }else if(entekhab == 9){
        string esm8;
        string famili8;
        string idd8;
        string ramzz8;
        int sal8;
        int mah8; 
        int rooz8;
        cout << " First name : ";
        cin >> esm8;
        cout << " Last name : ";
        cin >> famili8;
        cout << " Username : ";
        cin >> idd8;
        cout << " Password : ";
        cin >> ramzz8;
        cout << " Year of birth date : ";
        cin >> sal8;
        cout << " Month of birth date : ";
        cin >> mah8;
        cout << " Day of birth date : ";
        cin >> rooz8;
        person2.sign_Up(idd8,ramzz8,esm8,famili8,{sal8,mah8,rooz8},"Yes");
    }else if(entekhab == 10){
          string deleteaccount1;
          cout << "\n Enter the account name you want to delete : ";
          cin >> deleteaccount1;
          goodbye(deleteaccount1,"Persons.txt");
          cout << "\n The account has been deleted.\n";
    }
    }
    }


    









int main(){

    Person p1;
    cout << "\n Hello, Please login or sign up first.\n";
    First_Step(p1);
    
    
    




    return 0;
}
