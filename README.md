#codealpha_task-1
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

// Function to check if username already exists
bool usernameExists(string username) {
    ifstream file("users.txt");
    string user, pass;

    while (file >> user >> pass) {
        if (user == username) {
            file.close();
            return true;
        }
    }

    file.close();
    return false;
}

// Registration Function
void registerUser() {
    string username, password;

    cout << "\n========== Registration ==========\n";

    cout << "Enter Username: ";
    cin >> username;

    // Check duplicate username
    if (usernameExists(username)) {
        cout << "Error! Username already exists.\n";
        return;
    }

    cout << "Enter Password: ";
    cin >> password;

    // Validation
    if (username.length() < 4) {
        cout << "Username must be at least 4 characters.\n";
        return;
    }

    if (password.length() < 6) {
        cout << "Password must be at least 6 characters.\n";
        return;
    }

    ofstream file("users.txt", ios::app);
    file << username << " " << password << endl;
    file.close();

    cout << "Registration Successful!\n";
}

// Login Function
void loginUser() {
    string username, password;
    string user, pass;

    cout << "\n============= Login =============\n";

    cout << "Username: ";
    cin >> username;

    cout << "Password: ";
    cin >> password;

    ifstream file("users.txt");

    while (file >> user >> pass) {
        if (user == username && pass == password) {
            cout << "\nLogin Successful!";
            cout << "\nWelcome, " << username << "!\n";
            file.close();
            return;
        }
    }

    file.close();

    cout << "\nInvalid Username or Password!\n";
}

int main() {
    int choice;

    do {
        cout << "\n===================================";
        cout << "\n      LOGIN & REGISTRATION";
        cout << "\n===================================";
        cout << "\n1. Register";
        cout << "\n2. Login";
        cout << "\n3. Exit";
        cout << "\n\nEnter Choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            registerUser();
            break;

        case 2:
            loginUser();
            break;

        case 3:
            cout << "\nThank You!\n";
            break;

        default:
            cout << "\nInvalid Choice!\n";
        }

    } while (choice != 3);

    return 0;
}
