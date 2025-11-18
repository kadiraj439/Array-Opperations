# Non-Duplicated Integer Array Operations  
Name: Krish Adiraj  
Course: CISC 192 - C++ Programming  
Due Date: 11/02/2025  (Resubmitted 11/17/2025)
Assignment: Unique Integer Array Program

---

##  Program Description
Create a C++ program that:

Declares a fixed-size std::array<int, N> (you can choose N = 5 or any small number).
Prompts the user to enter unique integers (ensure no duplicates are allowed).
Displays a menu asking the user to perform one of the following operations:
(a) Sort the array in ascending order
(b) Sort the array in descending order
(c) Find the maximum number
Uses only manual sorting logic (e.g., nested loops).
Displays the results clearly after the operation.


Only `<iostream>` and `<array>` are used.  
Sorting is done manually using nested loops.

## Reflection

I originally forgot to include <array>, which caused compiler errors.

I first tried to use std::sort() but then realized it wasn’t allowed for this assignment.

My duplicate-checking didn’t work at first because I forgot to decrement i after a duplicate.

I mixed up the comparison signs in descending sort (> vs <).
After fixing the condition, the sorting worked correctly.

---

##  C++ Source Code

```cpp
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

        bool duplicate = false;
        for (int j = 0; j < i; j++) {
            if (numbers[j] == temp) {
                duplicate = true;
                break;
            }
        }

        if (duplicate) {
            cout << "Duplicate found, Enter a different number." << endl;
            i--; // go back one index
        } else {
            numbers[i] = temp;
        }
    }

    cout << "\nChoose an operation:\n";
    cout << "1. Sort Ascending\n";
    cout << "2. Sort Descending\n";
    cout << "3. Find Maximum\n";
    cout << "Enter your choice: ";

    int choice;
    cin >> choice;

    switch (choice) {
        case 1: {
            // Ascending sort
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
            for (int num : numbers) cout << num << " ";
            cout << endl;
            break;
        }
        case 2: {
            // Descending sort
            for (int i = 0; i < N - 1; i++) {
                for (int j = 0; j < N - i - 1; j++) {
                    if (numbers[j] < numbers[j + 1]) {
                        int temp = numbers[j];
                        numbers[j] = numbers[j + 1];
                        numbers[j + 1] = temp;
                    }
                }
            }

            cout << "\nArray sorted in descending order:\n";
            for (int num : numbers) cout << num << " ";
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
