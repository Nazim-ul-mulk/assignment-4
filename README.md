#include <iostream>
#include <string>
using namespace std;

class BankAccount {
private:
    int balance;
    string name;
public:
    BankAccount(string n, int b):name(n),balance(b) {
        cout << "Constructor called for " << n << endl;
        if (b < 0) {
            throw " balance cannot be negative";
        }
    }

    // withdraw function
    void withdraw(int amount) {
        cout << "Trying to withdraw money" << endl;

        if (amount > balance) {
            throw string("not enough balance");
        }

        balance -= amount;
        cout << "Withdrawal successful" << endl;
        cout<<"   Remaining balance is : " << balance << endl;
    }

    // destructor
    ~BankAccount() {
        cout << "Destructor called for " << name << endl;
    }
};

int main() {

    //exception in constructor
    try {
        BankAccount* acc1 = new BankAccount("NAZIM", -500);
        delete acc1;  
    }
    catch (const char* msg) {
        cout << "Exception caught in main: " << msg << endl;
    }
    //exception in withdraw function
    BankAccount* acc2 = NULL;

    try {
        acc2 = new BankAccount("IBTIASAM", 1000);
        acc2->withdraw(1500);
    }
    catch (string msg) {
        cout << "Exception caught in main: " << msg << endl;
    }

    delete acc2;
}
