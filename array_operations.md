// Name:Krish Adiraj
// Course: CISC 192 - C++ Programming
// Due Date: 11/02/2025
// Assignment: Non-Duplicated Integer Array Operations




#include <iostream>
#include <array>
using namespace std;

int main() {
    const int N = 5;
    array<int, N> numbers;
    int temp;
    
    cout << "Enter " << N << " unique integers:" << endl;
    
    // Input loop
    for (int i = 0; i < N; i++) {
        cout << "Element " << i + 1 << ": ";
        cin >> temp;
        
        // check duplicates
        bool duplicate = false;
        for (int j = 0; j < i; j++) {
            if (numbers[j] == temp) {
                duplicate = true;
                break;
            }
        }
        
        if (duplicate) {
            cout << "Duplicate found, Enter a different number." << endl;
            i--; // go back one index to replace it
        } else {
            numbers[i] = temp;
            // I didn’t use i-- when I found a duplicate, so it skipped one number before.
        }
    }

    // Menu
    cout << "\nChoose a operation:\n";
    cout << "1. Sort Ascending\n";
    cout << "2. Sort Descending\n";
    cout << "3. Find Maximum\n";
    cout << "Enter your choice: ";
    int choice;
    cin >> choice;

    switch (choice) {
        case 1: {
            // Sort Ascending (bubble sort)
            for (int i = 0; i < N - 1; i++) {
                for (int j = 0; j < N - i - 1; j++) {
                    if (numbers[j] > numbers[j + 1]) {
                        int temp = numbers[j];
                        numbers[j] = numbers[j + 1];
                        numbers[j + 1] = temp;
                    }
                }
            }

            cout << "\nArray sorted in ascending order:\n";
            for (int i = 0; i < N; i++) {
                cout << numbers[i] << " ";
            }
            cout << endl;
            break;
        }
        case 2: {
            // Sort Descending
            for (int i = 0; i < N - 1; i++) {
                for (int j = 0; j < N - i - 1; j++) {
                    if (numbers[j] < numbers[j + 1]) { // flipped sign
                        int temp = numbers[j];
                        numbers[j] = numbers[j + 1];
                        numbers[j + 1] = temp;
                    }
                }
            }

            cout << "\nArray sorted in descending order:\n";
            for (int i = 0; i < N; i++) {
                cout << numbers[i] << " ";
            }
            cout << endl;
            break;
        }
        case 3: {
            int max = numbers[0];
            for (int i = 1; i < N; i++) {
                if (numbers[i] > max) {
                    max = numbers[i];
                }
            }
            cout << "\nThe maximum number is: " << max << endl;
            break;
        }
        default:
            cout << "Invalid choice, Please run the program again." << endl;
    }

    return 0;
}


When I started this, I kept getting compiler errors because I forgot to include `<array>`.  
Then I accidentally used `std::sort()` before realizing it wasn’t allowed.  

My biggest mistake was not checking duplicates properly — it just kept accepting the same number twice.  
I fixed that by using a nested loop and adding `i--` when a duplicate was found.

Also, I messed up the descending sort the first time because I compared with `>` instead of `<`.  
Now it sorts correctly.  
