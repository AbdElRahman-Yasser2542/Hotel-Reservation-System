# Hotel-Reservation-System
# A C++ console-based hotel reservation system that allows users to view room availability, reserve and cancel rooms, display current reservations, and search for customers. The project demonstrates programming fundamentals, including arrays, functions, loops, conditional statements, and switch-case menus.
#include <iostream>
#include <string>

using namespace std;

/* =========================================
   PERSON 1
   Variables + Arrays + Show Rooms
========================================= */

const int SIZE = 5;

int roomNumber[SIZE] = {101, 102, 103, 104, 105};

bool booked[SIZE] = {false, false, false, false, false};

string customerName[SIZE] = {"", "", "", "", ""};


// Function to show room status
void showRooms()
{
    cout << "\n------ Room Status ------\n";

    for(int i = 0; i < SIZE; i++)
    {
        cout << "Room " << roomNumber[i] << " : ";

        if(booked[i] == true)
        {
            cout << "Booked";
        }
        else
        {
            cout << "Available";
        }

        cout << endl;
    }
}



/* =========================================
   PERSON 2
   Reserve Room Function
========================================= */

void reserveRoom()
{
    int room;
    string name;

    cout << "\nEnter Room Number: ";
    cin >> room;

    for(int i = 0; i < SIZE; i++)
    {
        if(room == roomNumber[i])
        {
            if(booked[i] == false)
            {
                cin.ignore();

                cout << "Enter Customer Name: ";
                getline(cin, name);

                customerName[i] = name;

                booked[i] = true;

                cout << "Room Reserved Successfully.\n";
            }
            else
            {
                cout << "Room Already Booked.\n";
            }

            return;
        }
    }

    cout << "Room Not Found.\n";
}



/* =========================================
   PERSON 3
   Cancel Reservation Function
========================================= */

void cancelReservation()
{
    int room;

    cout << "\nEnter Room Number to Cancel: ";
    cin >> room;

    for(int i = 0; i < SIZE; i++)
    {
        if(room == roomNumber[i])
        {
            if(booked[i] == true)
            {
                booked[i] = false;

                customerName[i] = "";

                cout << "Reservation Cancelled.\n";
            }
            else
            {
                cout << "Room is already empty.\n";
            }

            return;
        }
    }

    cout << "Room Not Found.\n";
}



/* =========================================
   PERSON 4
   Show Reservations + Search Customer
========================================= */

// Function to show reservations
void showReservations()
{
    cout << "\n------ Reservations ------\n";

    for(int i = 0; i < SIZE; i++)
    {
        if(booked[i] == true)
        {
            cout << "Room " << roomNumber[i]
                 << " reserved by "
                 << customerName[i] << endl;
        }
    }
}


// Function to search customer
void searchCustomer()
{
    string name;

    cin.ignore();

    cout << "\nEnter Customer Name: ";

    getline(cin, name);

    for(int i = 0; i < SIZE; i++)
    {
        if(customerName[i] == name)
        {
            cout << "Customer Found in Room "
                 << roomNumber[i] << endl;

            return;
        }
    }

    cout << "Customer Not Found.\n";
}



/* =========================================
   PERSON 5
   Main Function + Menu + Switch
========================================= */

int main()
{
    int choice;

    do
    {
        cout << "\n===== Hotel Reservation System =====\n";

        cout << "1. Show Rooms\n";
        cout << "2. Reserve Room\n";
        cout << "3. Cancel Reservation\n";
        cout << "4. Show Reservations\n";
        cout << "5. Search Customer\n";
        cout << "6. Exit\n";

        cout << "Enter Your Choice: ";

        cin >> choice;

        switch(choice)
        {
            case 1:
                showRooms();
                break;

            case 2:
                reserveRoom();
                break;

            case 3:
                cancelReservation();
                break;

            case 4:
                showReservations();
                break;

            case 5:
                searchCustomer();
                break;

            case 6:
                cout << "Program Ended.\n";
                break;

            default:
                cout << "Invalid Choice.\n";
        }

    } while(choice != 6);

    return 0;
}
