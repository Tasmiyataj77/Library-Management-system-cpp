#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Structure to represent a book
struct Book {
    int id;
    string title;
    string author;
    bool isIssued;
};

// Class to manage library operations
class Library {
private:
    vector<Book> books;

public:
    // Function to add a new book
    void addBook() {
        Book newBook;
        cout << "Enter book ID: ";
        cin >> newBook.id;
        cout << "Enter book title: ";
        cin.ignore();
        getline(cin, newBook.title);
        cout << "Enter book author: ";
        getline(cin, newBook.author);
        newBook.isIssued = false;
        books.push_back(newBook);
        cout << "Book added successfully!\n";
    }

    // Function to display all books
    void displayBooks() {
        if (books.empty()) {
            cout << "No books available in the library.\n";
            return;
        }

        cout << "\nBooks in the library:\n";
        for (const auto& book : books) {
            cout << "ID: " << book.id << ", Title: " << book.title
                 << ", Author: " << book.author << ", Issued: " 
                 << (book.isIssued ? "Yes" : "No") << "\n";
        }
    }

    // Function to issue a book
    void issueBook() {
        int id;
        cout << "Enter book ID to issue: ";
        cin >> id;

        for (auto& book : books) {
            if (book.id == id) {
                if (!book.isIssued) {
                    book.isIssued = true;
                    cout << "Book issued successfully!\n";
                } else {
                    cout << "Book is already issued.\n";
                }
                return;
            }
        }
        cout << "Book not found!\n";
    }

    // Function to return a book
    void returnBook() {
        int id;
        cout << "Enter book ID to return: ";
        cin >> id;

        for (auto& book : books) {
            if (book.id == id) {
                if (book.isIssued) {
                    book.isIssued = false;
                    cout << "Book returned successfully!\n";
                } else {
                    cout << "This book was not issued.\n";
                }
                return;
            }
        }
        cout << "Book not found!\n";
    }

    // Function to delete a book
    void deleteBook() {
        int id;
        cout << "Enter book ID to delete: ";
        cin >> id;

        for (auto it = books.begin(); it != books.end(); ++it) {
            if (it->id == id) {
                books.erase(it);
                cout << "Book deleted successfully!\n";
                return;
            }
        }
        cout << "Book not found!\n";
    }
};

// Main function to interact with the library system
int main() {
    Library library;
    int choice;

    do {
        cout << "\nLibrary Management System\n";
        cout << "1. Add Book\n";
        cout << "2. Display All Books\n";
        cout << "3. Issue Book\n";
        cout << "4. Return Book\n";
        cout << "5. Delete Book\n";
        cout << "6. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            library.addBook();
            break;
        case 2:
            library.displayBooks();
            break;
        case 3:
            library.issueBook();
            break;
        case 4:
            library.returnBook();
            break;
        case 5:
            library.deleteBook();
            break;
        case 6:
            cout << "Exiting system...\n";
            break;
        default:
            cout << "Invalid choice! Please try again.\n";
        }
    } while (choice != 6);

    return 0;
}
