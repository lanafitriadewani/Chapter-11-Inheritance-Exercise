#include<iostream>
using namespace std;

class bankAccount
{
public:
    int accountNumber;
    double balance;
    
    bankAccount(int an,double bal)
    {
        accountNumber=an;
        balance=bal;
    }
    bankAccount()
    {
    
    }
    double getBalance()
    {
        return(balance);
    }
    int getAccountNumber()
    {
        return(accountNumber);
    }
    void setBalance(double amount)
    {
        balance=amount;
    }
    void setAccountNumber(int ano)
    {
        accountNumber=ano;
    }
    void virtual showAccountInfo()
    {
        cout<<"Account Number : "<<accountNumber<<endl;
        cout<<"Account Balance: "<<balance<<endl;
    }
    double virtual depositAmount(double damount)
    {
        balance=balance+damount;
        return(balance);
    }
    double virtual withDrawAmount(double wamount)
    {
        balance=balance-wamount;
        return(balance);
    }
};

class checkingAccount : bankAccount
{
    double interest, min_Bal,serviceCharge;

public: 
    checkingAccount(int _an,double _at,double _interest):bankAccount(_an,_at)
    {
        interest=_interest;
        min_Bal=500;
    }
    void setInterestRate(double irate)
    {
        interest=irate;
    }
    double retrieveInterestRate()
    {
        return(interest);
    }
    void setMinBal(double m_bal)
    {
        min_Bal=m_bal;
    }
    double retrieveMinBal()
    {
        return(min_Bal);
    }
    void setServiceCharge(double scharge)
    {
        serviceCharge=scharge;
    }
    double retrieveServiceCharge()
    {
        return(serviceCharge);
    }
    double depositAmount(double damount)
    {
        balance=balance+damount;
        return(balance);
    }
    double withDrawAmount(double wamount)
    {
        if(check())
            balance=balance-wamount;
        else
            cout<<"You have in sufficient balance"<<endl;
            return(balance);
    }
    bool check()
    {
        if(balance<min_Bal)
            return(false);
        else
            return(true);
    }
    void showAccountInfo()
    {
        cout<<"Account Number : "<<accountNumber<<endl;
        cout<<"Account Balance: "<<balance<<endl;
    }
};

class savingAccount:bankAccount
{
    double min_Bal;
public:
    savingAccount(int _a,double _at):bankAccount(_a,_at)
    {
        min_Bal=500;
    }
    double depositAmount(double damount)
    {
        balance=balance+damount;
        return(balance);
    }
    double withDrawAmount(double wamount)
    {
        if(check())
        balance=balance-wamount;
        else
        cout<<"You have in sufficient balance"<<endl;
        return(balance);
    }
    void setMinBal(double mbal)
    {
        min_Bal=mbal; 
    }
    bool check()
    {
        if(balance<min_Bal)
        return(false);
        else
        return(true);
    }
    void showAccountInfo()
    {
        cout<<"Account Number : "<<accountNumber<<endl;
        cout<<"Account Balance: "<<balance<<endl;
    }
};

int main()
{
    double amount;
    int choice;
    
    do
    {
        cout<<endl;
        cout<<"Create an Account"<<endl;
        cout<<"1 Checking Account"<<endl;
        cout<<"2 Saving Account"<<endl;
        cout<<"3 Exit"<<endl;
        cin>>choice;
        
        if(choice==1)
        {
            cout<<endl<<"Enter account number: ";
            int ano;
            cin>>ano;
            cout<<endl<<"Enter opening balance: ";
            double obal;
            cin>>obal;
            double irate;
            cout<<endl<<"Enter interest rate: ";
            cin>>irate;
            checkingAccount ox(ano,obal,irate);
            int ch;
            
            do
            {
                cout<<endl<<"1 Deposit "<<endl<<"2 WithDraw"<<endl<<"3 Account Info"<<endl<<"4 Exit"<<endl;
                cin>>ch;
                switch(ch)
                {
                    case 1:
                    cout<<endl<<"Enter amount: ";
                    cin>>amount;
                    double damount;
                    damount=ox.depositAmount(amount);
                    cout<<"Available balance: "<<damount<<endl;
                    break;
                    
                    case 2:
                    cout<<endl<<"Enter amount: ";
                    cin>>amount;
                    double wamount;
                    wamount=ox.withDrawAmount(amount);
                    cout<<"Available balance: "<<wamount<<endl;
                    break;
                    
                    case 3:
                    cout<<endl;
                    ox.showAccountInfo();
                    break;
                }
            }
            
            while(ch!=4);
        }
        
        else if(choice==2)
        {
            cout<<endl<<"Enter account number: ";
            int _a;
            cin>>_a;
            cout<<endl<<"Enter opening balance: ";
            double _obal;
            cin>>_obal;
            double _irate;
            cout<<endl<<"Enter interest rate: ";
            cin>>_irate;
            savingAccount sOx(_a,_obal);
            int _ch;
            
            do
            {
                cout<<endl<<"1 Deposit"<<endl<<"2 WithDraw"<<endl<<"3 Account Info"<<endl<<"4 Exit"<<endl;
                cin>>_ch;
                switch(_ch) 
                {
                    case 1:
                    cout<<endl<<"Enter amount: ";
                    cin>>amount;
                    double _damount;
                    _damount=sOx.depositAmount (amount);
                    cout<<"Available balance: "<<_damount<<endl;
                    break;
                    
                    case 2:
                    cout<<endl<<"Enter amount: ";
                    cin>>amount;
                    double _wamount;
                    _wamount=sOx.withDrawAmount(amount);
                    cout<<"Available balance: "<<_wamount<<endl;
                    break;
                    
                    case 3:
                    cout<<endl;
                    sOx.showAccountInfo();
                    break;
                    
                    case 4:
                    break;
                    default:cout<<endl<<"Invalid choice";
                    break;
                }
            }
            
            while(_ch!=4);
        }
    }
    
    while(choice!=3);
}
