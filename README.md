# Master C++ programming on Linux

Resources: https://www.youtube.com/watch?v=TZANnCMJxUE&list=PLKMOdY6Bhga5ws13FNCbD0103pXEP-VFV

 ## Intro - Why learning C++?

  * Efficient + performance: full access to RAM
  * portability -> any system (anywhere)
  * stable -> 40 years (System V)
  * standardization

## Part 1- Environment Setup

- Install VS Code
- Install Packages in VS Code:
  - **C/C++ IntelliSense** from Microsoft, with 70M downloads.
  - **Code Runner** from Jun Han with 29M downloads
  - **C/C++ Makefile Project** from Adriano Markovic with 140k downloads or the Microsoft version with 5.5M downloads

* Optionally install gcc compiler only if Ubuntu/Debian has not brought it up

  ```shell
  sudo apt install build-essential gdb
  gcc --version
  
  ## For ArchLinux, the command is:
  ## sudo pacman -S base-devel
  ```



## Part 2- Hello World app

 - ```cpp
   #include <iostream>
   
   int main(){
   
       std::cout << "Hello World!" << std::endl;
       return 0;
   
   }
   ```



### - Install C/C++ makefile

* Features of `makefile`
  * automation of Build Process
  * manage dependencies
  * compile/build multiple sources
  * keeps track of compilations
* 



### - Using make

* configure the Makefile

* move main.cpp to `src` folder

* from terminal 

  ```shell
  make
  ```

* ### Run the app

  ```shell
  SimpleList
  ```



## Part 3 - Making our C++ Program

* args

  * arg[0] <- program name

  * arg[1] <- 1st arg

  * ...

  * arg[n] <- nth arg

* User input
* Make better choice program



## Part 4 - Vectors 

The cpp is as below so far:

```cpp
#include <iostream>
#include <vector>
using namespace std;

void print_menu(string name);
void print_list();
void add_item();
void delete_item();

vector<string> list;
string name;

int main(int arg_count, char *args[]){

    if(arg_count > 1) {
        name = string(args[1]);
        print_menu(name);
    }
    else {
        cout << "Username not supplied.. exiting the program" << endl;
    }

    return 0;

}

void print_menu(string name){
    int choice;

    cout << "***************\n";
    cout << " 1 - Print list.\n";
    cout << " 2 - Add to list.\n";
    cout << " 3 - Delete from list.\n";
    cout << " 4 - Quit.\n";
    cout << " Enter your choice and press return/enter.\n";

    cin >> choice;

    if(choice == 4 ) {
        exit(0);
    }
    else {
        cout << "Sorry choice hasn't been implemented.\n";
    }
}

void add_item(){

    cout << "\n\n\n\n\n";
    cout << "*** Add Item ***";
    cout << "Type in an item and press enter: ";

    string item;
    cin >> item;

    list.push_back(item);

    cout << "Successfully added an item to the list \n\n\n\n";
    cin.clear();

    print_menu(name);
}
```



## Part 5- Adding Menu Choices

Here you are:

```cpp
#include <iostream>
#include <vector>
using namespace std;

void print_menu(string name);
void print_list();
void add_item();
void delete_item();

vector<string> list;
string name;

int main(int arg_count, char *args[]){

    if(arg_count > 1) {
        name = string(args[1]);
        print_menu(name);
    }
    else {
        cout << "Username not supplied.. exiting the program" << endl;
    }

    return 0;

}

void print_menu(string name){
    int choice;

    cout << "***************\n";
    cout << " 1 - Print list.\n";
    cout << " 2 - Add to list.\n";
    cout << " 3 - Delete from list.\n";
    cout << " 4 - Quit.\n";
    cout << " Enter your choice and press return/enter.\n";

    cin >> choice;

    if(choice == 4 ) {
        exit(0);
    }
    else if(choice == 3 ){
        delete_item();
    }
    else if(choice == 2 ){
        add_item();
    }
    else if(choice == 1 ) {
        print_list();
    }
    else {
        cout << "Sorry choice hasn't been implemented.\n";
    }
}

void add_item(){

    cout << "\n\n\n\n\n";
    cout << "*** Add Item ***\n";
    cout << "Type in an item and press enter: \n";

    string item;
    cin >> item;

    list.push_back(item);

    cout << "Successfully added an item to the list \n\n\n\n";
    cin.clear();

    print_menu(name);
}

void delete_item() {
    
    cout << "*** Delete Item ***\n";
    cout << "Select an item index to delete\n";

    if(list.size()) {
        for(int i=0; i < list.size(); i++) {
            cout << i << ": " << list[i] << "\n";
        }
    }
    else {
        cout << "No items in the list or to delete.\n";
    }

    print_menu(name);
    
}

void print_list() {

    cout << "\n\n\n\n\n\n";
    cout << "*** Printing List ***\n";

    for(int list_index=0; list_index < list.size(); list_index++) {
        cout << " * " << list[list_index] << "\n";
    }

    cout << "M - Menu \n";
    char choice;
    cin >> choice;

    if( choice == 'M' || choice == 'm'){
        print_menu(name);
    }
    else {
        cout << "Invalid Choice. Quitting...\n";
    }
}
```



## Part 6 - Classes and Objects



Fix the issue of warning by type cast, fir instance: at line 96, add `int()` to `list.size()` as:

```cpp
for(int list_index=0; list_index < int(list.size()); list_index++){
	cout << " * " << list[list_index] << "\n";
}
```

But type casting may lose the precision, then a better way is to `unsign` the list_index as below:

```cpp
for(unsigned int list_index=0; list_index < list.size(); list_index++){
	cout << " * " << list[list_index] << "\n";
}
```

### Classes and Objects

Add a header file in `src/include/` folder: `src/include/list.h`

`src/include/list.h` file:

```cpp
#include <iostream>
#include <vector>
using namespace std;

class List {
    private:

    protected:

    public:

        List() {
            //constructor
        }
        ~List() {
            //destructor
        }

        vector<string> list;
        string name;

        void print_menu();
        void print_list();
        void add_item();
        void delete_item();
};
```



`src/list.cpp` file:

```cpp
#include "include/list.h"

void List::print_menu() {
    int choice;

    cout << "***************\n";
    cout << " 1 - Print list.\n";
    cout << " 2 - Add to list.\n";
    cout << " 3 - Delete from list.\n";
    cout << " 4 - Quit.\n";
    cout << " Enter your choice and press return/enter.\n";

    cin >> choice;

    if(choice == 4 ) {
        exit(0);
    }
    else if(choice == 3 ){
        delete_item();
    }
    else if(choice == 2 ){
        add_item();
    }
    else if(choice == 1 ) {
        print_list();
    }
    else {
        cout << "Sorry choice hasn't been implemented.\n";
    }
}

void List::add_item(){

    cout << "\n\n\n\n\n";
    cout << "*** Add Item ***\n";
    cout << "Type in an item and press enter: \n";

    string item;
    cin >> item;

    list.push_back(item);

    cout << "Successfully added an item to the list \n\n\n\n";
    cin.clear();

    print_menu();
}

void List::delete_item() {
    
    cout << "*** Delete Item ***\n";
    cout << "Select an item index to delete\n";

    if(list.size()) {
        for(unsigned int i=0; i < list.size(); i++) {
            cout << i << ": " << list[i] << "\n";
        }
    }
    else {
        cout << "No items in the list or to delete.\n";
    }

    print_menu();
    
}

void List::print_list() {

    cout << "\n\n\n\n\n\n";
    cout << "*** Printing List ***\n";

    for(unsigned int list_index=0; list_index < list.size(); list_index++) {
        cout << " * " << list[list_index] << "\n";
    }

    cout << "M - Menu \n";
    char choice;
    cin >> choice;

    if( choice == 'M' || choice == 'm'){
        print_menu();
    }
    else {
        cout << "Invalid Choice. Quitting...\n";
    }
}
```



`src/main.cpp` file:

```cpp
#include "include/list.h"

int main(int arg_count, char *args[]){

    if(arg_count > 1) {
        List simpleList;
        simpleList.name = string(args[1]);
        simpleList.print_menu();
    }
    else {
        cout << "Username not supplied.. exiting the program" << endl;
    }

    return 0;

}
```



## Part 7- Source Control with Git

Plus update the delete_item function:
```cpp
void List::delete_item() {
    
    cout << "*** Delete Item ***\n";
    cout << "Select an item index to delete: \n";

    if(list.size()) {
        for(unsigned int i=0; i < list.size(); i++) {
            cout << i << ": " << list[i] << "\n";
        }
        int choiceNum;
        cin >> choiceNum;
        list.erase(list.begin()+choiceNum);
    }
    else {
        cout << "No items in the list or to delete.\n";
    }

    print_menu();
    
}
```

## Part 8 - Making a Database 01:49
Please check the database.h and database.cpp, plus main.cpp
```cpp
void Database::write() {
    ofstream db;
    db.open("db/lists.sl");

    if(db.is_open()) {
        db << "1\n2\n3\n4\n5\n";
    }
    else {
        cout << "Cannot open file for writing.\n";
    }

    db.close();
}
```

## Part 9 - Write and read the databse 1:59
resume to function Database.read():
```cpp
void Database::read(){
    string line;
    ifstream db;
    db.open("db/lists.sl");

    if(db.is_open()) {
        while(getline(db,line,'\n')) {
            cout << line << "\n";
        }
    }
    else {
        cout << "Cannot open file for reading.\n";
    }

    db.close();
}
```
### Difference of double quote and single quote

- double quote "" is for string, or array of characters
- single quote '' is for char, or single character

then `\n` is a sinle char and should associate with single quote.

After testing okay with writing and reading the numbers, also try write the simpleList.list to the database.

## Part 10 - User Management in Database - 02:11


## Part 11 - Fully Working Program - 02:35
Here are the codes so far:

- main.cpp:
```cpp
#include "include/list.h"
#include "include/database.h"

int main(int arg_count, char *args[]){

    List simpleList;
    Database data;

    if(arg_count > 1) {
        simpleList.name = string(args[1]);
        simpleList.mainList = data.read();
        simpleList.find_userList();
        simpleList.print_menu();
        data.write(simpleList.mainList);
    }
    else {
        cout << "Username not supplied.. exiting the program" << endl;
    }

    return 0;

}
```

- database.cpp:
```cpp
#include "include/database.h"

void Database::write(vector<vector<string>> mainList) {

    ofstream db;
    db.open("db/lists.sl");

    if(db.is_open()) {
        for( unsigned int user_index=0; user_index < mainList.size(); user_index++ ) {
            for( unsigned int list_index=0; list_index < mainList[user_index].size(); list_index++ ) {
                if( list_index == 0 ) {
                    db << "#" << mainList[user_index][list_index] << "\n";
                }
                else {
                    db << mainList[user_index][list_index] << "\n";
                }
            }
            db << "%" << "\n";
        }
    }
    else {
        cout << "Cannot open file for writing.\n";
    }

    db.close();

}

vector<vector<string>> Database::read(){
    string line;
    ifstream db;

    vector<string> userList;

    db.open("db/lists.sl");

    if(db.is_open()) {
        while(getline(db,line,'\n')) {
            if(line.front() == '#') {
                cout << "Found a hashtag: " << line << "\n";
                line.erase(line.begin());
                userList.push_back(line);

            }
            else if(line.front() == '%') {
                cout << "Found a percentage: " << line << "/n";
                mainList.push_back(userList);
                userList.clear();
            }
            else {
                cout << "Found an item: " << line << "\n";
                userList.push_back(line);

            }
        }
    }
    else {
        cout << "Cannot open file for reading.\n";
    }

    db.close();

    return mainList;
}
```

- list.cpp:
```cpp
#include "include/list.h"

void List::print_menu() {
    int choice;

    cout << "***************\n";
    cout << " 1 - Print list.\n";
    cout << " 2 - Add to list.\n";
    cout << " 3 - Delete from list.\n";
    cout << " 4 - Save list.\n";
    cout << " 5 - Quit.\n";
    cout << " Enter your choice and press return/enter.\n";

    cin >> choice;

    if(choice == 5 ) {
        return;
    }
    else if(choice == 4 ) {
        save_list();
    }
    else if(choice == 3 ){
        delete_item();
    }
    else if(choice == 2 ){
        add_item();
    }
    else if(choice == 1 ) {
        print_list();
    }
    else {
        cout << "Sorry choice hasn't been implemented.\n";
    }
}

void List::add_item(){

    cout << "\n\n\n\n\n";
    cout << "*** Add Item ***\n";
    cout << "Type in an item and press enter: \n";

    string item;
    cin >> item;

    list.push_back(item);

    cout << "Successfully added an item to the list \n\n\n\n";
    cin.clear();

    print_menu();
}

void List::delete_item() {
    
    cout << "*** Delete Item ***\n";
    cout << "Select an item index to delete: \n";

    if(list.size()) {
        for(unsigned int i=0; i < list.size(); i++) {
            cout << i << ": " << list[i] << "\n";
        }
        int choiceNum;
        cin >> choiceNum;
        list.erase(list.begin()+choiceNum);
    }
    else {
        cout << "No items in the list or to delete.\n";
    }

    print_menu();
    
}

void List::print_list() {

    cout << "\n\n\n\n\n\n";
    cout << "*** Printing List ***\n";

    for(unsigned int list_index=0; list_index < list.size(); list_index++) {
        cout << " * " << list[list_index] << "\n";
    }

    cout << "M - Menu \n";
    char choice;
    cin >> choice;

    if( choice == 'M' || choice == 'm'){
        print_menu();
    }
    else {
        cout << "Invalid Choice. Quitting...\n";
    }
}

bool List::find_userList() {
    bool userFound = false;

    cout << "\n\n\n\n\n\n";
    cout << "*** Welcome " << name << " ***\n";

    for(unsigned int user_index=0; user_index < mainList.size(); user_index++ ) {
        cout << mainList[user_index][0] << "\n";
        if(mainList[user_index][0] == name) {
            cout << "User has been found: " << mainList[user_index][0] << "\n";
            list = mainList[user_index];
            currentUserIndex = user_index;
            userFound = true;
            break;
        }
    }

    if(userFound == false) {
        list.push_back(name);
        mainList.push_back(list);
        currentUserIndex = mainList.size() - 1;
    }

    return userFound;
}

void List::save_list() {
    cout << "Saving the list...\n";
    mainList[currentUserIndex] = list;
    print_menu();
}
```

- include/database.h
```cpp
#include <iostream>
#include <vector>
#include <fstream>

using namespace std;

class Database {
    private:

    protected:

    public:

        Database() {
            //constructor
        }
        ~Database() {
            //destructor
        }

        vector<vector<string>> mainList;
        string name;

        void write(vector<vector<string>> mainList);
        vector<vector<string>> read();
};
```

- include/list.h
```cpp
#include <iostream>
#include <vector>
#include <fstream>

using namespace std;

class Database {
    private:

    protected:

    public:

        Database() {
            //constructor
        }
        ~Database() {
            //destructor
        }

        vector<vector<string>> mainList;
        string name;

        void write(vector<vector<string>> mainList);
        vector<vector<string>> read();
};
```

- db/list.sl
```cpp
#Marcus
Item1
Item2
Item3
Item4
%
#Jennifer
Item4
Item5
Item6
%

```

## Part 12 - Cleaning up - 02:47

## Part 13 - Debugging - 02:53