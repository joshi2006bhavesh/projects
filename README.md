#include<iostream>
#include<string>
using namespace std;
class Node
{
    public:
    string name;
    int roll;
    string dept; //dept = department in which child is currently in 
    int marks ;
    Node* next;

        //constructor
        Node(int roll)
        {
            this->roll = roll;
            this->name = "";
            this->dept = "";
            this->marks= -1 ;
            this->next = NULL;         
        }
};
//function for checking whether the student record is available or not 
bool check(Node* head , int x)
{
    Node* temp = head;
    if(temp == NULL)
    {
        return false;
    }
    else
    {
        while(temp!=NULL)
        {
            if(temp->roll == x)
            {
                return true;
            }
            temp = temp->next;
        }
    }
    return false;
}
//inserting a new record for student with a roll number 
void insertion(Node*& head,int x,string name1,string dept1,int marks1)
{
//checking wether the record already exists
if(check(head,x) == true)
{
    cout<<"Sorry but the record already exists for this roll number ! "<<endl;
    cout<<endl<<endl<<endl;
    return ;
}
Node* prev = new Node(0);
Node* temp = head;

//entering the information of the student which has to be addded 
                    Node* student = new Node(x);
                    student->name = name1;
                    student->dept = dept1;
                    student->marks = marks1;

prev->next = temp;

//adding at starting just after NULL
if(temp==NULL)
{
    head = student;
    cout<<"Record added successfully ! "<<endl;
    cout<<endl<<endl<<endl;
}
else
{
    while(temp!=NULL)
    {
        //adding in start but the database alreaddy have some data
        if(prev == NULL && temp->roll > student->roll)
        {
            student->next = temp;
            prev->next = NULL;
            cout<<"Record added successfully "<<endl;
            cout<<endl<<endl<<endl;
            return;
        }
        //adding in between 
        if(student->roll>prev->roll && student->roll<temp->roll)
        {
            prev->next = NULL;
            prev->next = student;
            student->next = temp;
            cout<<"Record added successfully "<<endl;
            cout<<endl<<endl<<endl;
            return;
        }
        prev = temp;
        temp = temp->next;
        //adding at last;
        if(student->roll>prev->roll && temp==NULL)
        {
            prev->next = student;
            student->next = NULL;
            cout<<"Record added successfully "<<endl;
            cout<<endl<<endl<<endl;
            return;
        }
    }
}
}
//function used for searching a record for a student 
void searchrecord(Node* head,int x)
{
    Node* temp = head;

    if(temp == NULL)
    {
        cout<<"The record is not available ! "<<endl;
        cout<<endl<<endl<<endl;
        return;
    }
    while(temp!=NULL)
    {
        if(temp->roll == x)
        {   
            cout<<endl<<endl<<endl;
            cout<<"Roll no of student :- "<<temp->roll<<endl;
            cout<<"Name of student :- "<<temp->name<<endl;
            cout<<"Deptarment :- "<<temp->dept<<endl;
            cout<<"Marks obtained :- "<<temp->marks<<endl;
            cout<<endl<<endl<<endl;
            return;
        }
        temp=temp->next;
    }
    cout<<"The record was not found ! "<<endl;
    cout<<endl<<endl<<endl;
}
//function used for deletion of record 
void deletion(Node*& head , int x)
{
    //checking wether the record is available or not 
    if(check(head,x) == false)
    {
        cout<<"Sorry but the record was not found ! "<<endl;
        cout<<endl<<endl<<endl;
        return;
    }
    else
    {
        Node* temp = head;
        Node* prev = new Node(0);
        prev->next = temp;
        while(temp != NULL)
        {
            //if the student that has to be deleted lies in between 
            if(prev->roll<x && temp->roll == x)
            {
                prev->next = temp->next;
                temp->next = NULL;
                head = prev;
                cout<<"The record was deleted successfully ! "<<endl;
                cout<<endl<<endl<<endl;
                return;
            }
            prev = temp;
            temp = temp->next;
            // if the student that has to be deleted is in last 
            if(temp == NULL && prev->roll == x)
            {
                prev->next = NULL;
                cout<<"The record was deleted successfully ! "<<endl;
                cout<<endl<<endl<<endl;
                return;
            }
        }
    }
}
int main()
{
    Node* node = NULL;
    Node* head = node;
    int val;

    //basic structure of intro starts from here

    while(true)
    {
        cout<<"******************** WELCOME TO THE STUDENT RECORD MANAGEMENT SYSTEM ********************"<<endl;
        cout<<endl<<endl;
        cout<<"Press 1 for checking for a record . "<<endl;
        cout<<"Press 2 for insertion of a record in the database . "<<endl;
        cout<<"Press 3 for searching for a record . "<<endl;
        cout<<"Press 4 for deletion of a record . "<<endl;
        cout<<"Press 5 to Exit . "<<endl;
        cout<<endl<<endl;
        cout<<"******************************************************************************************"<<endl;
        cout<<endl<<endl<<endl;

        cin>>val;
        cout<<endl<<endl;
        if(val==1)
        {
            cout<<"Enter the roll no to search for !"<<endl;
            int x;
            cin>>x;
            if(check(head , x))
            {
                cout<<"The record was found successfully ! "<<endl;
                cout<<endl<<endl<<endl;
            }
            else
            {
                cout<<"The record was not found ! "<<endl;
                cout<<endl<<endl<<endl;
            }
        }
        else if(val == 2)
        {
            cout<<"For adding a record please enter the following information !"<<endl;
            cout<<"Enter the roll no ! "<<endl;
            int x;
            cin>>x;
            cout<<"Enter the name of the student ! "<<endl;
            string name1;
            cin>>name1;
            cout<<"Enter the department to which student belongs ! "<<endl;
            string dept1;
            cin>>dept1;
            cout<<"Enter the total number of marks obtained by the student ! "<<endl;
            int marks1;
            cin>>marks1;
            insertion(head,x,name1,dept1,marks1);
        }
        else if(val == 3)
        {
            cout<<"Enter the roll no to search for ! "<<endl;
            int x;
            cin>>x;
            searchrecord(head,x);
        }
        else if(val == 4)
        {   
            cout<<"Enter the roll no for you want to delete the database !"<<endl;
            int x;
            cin>>x;
            deletion(head , x);
        }
        else if(val == 5)
        {
            cout<<"Feel free to ask from any other assistance ! Thank You (^_^)";
            break;
        }
    } 
    return 0;
}
