# Library
```mermaid
classDiagram
    class Book {
        <<interface>>
        + getTitle(): String
        + getAuthor(): String
        + getISBN(): String
        + isAvailable(): Boolean
    }

    class PrintedBook {
        - ISBN: String
        - title: String
        - author: String
        - publisher: String
        - availability: Boolean
        + getTitle(): String
        + getAuthor(): String
        + getISBN(): String
        + isAvailable(): Boolean
        + issue(): void
        + return(): void
    }

    class EBook {
        - ISBN: String
        - title: String
        - author: String
        - fileSize: Double
        - format: String
        - downloadLink: String
        + getTitle(): String
        + getAuthor(): String
        + getISBN(): String
        + isAvailable(): Boolean
        + download(): void
    }

    class Library {
        - name: String
        - address: String
        - books: List<Book>
        - members: List<Member>
        - librarians: List<Librarian>
        + addBook(book: Book)
        + removeBook(book: Book)
        + registerMember(member: Member)
        + issueBook(book: Book, member: Member)
        + returnBook(book: Book, member: Member)
    }

    class Member {
        - memberID: String
        - name: String
        - contactInfo: String
        - borrowedBooks: List<Book>
        - isActive: Boolean
        + register(name: String, contactInfo: String): Member
        + borrowBook(book: Book): void
        + returnBook(book: Book): void
    }

    class Librarian {
        - employeeID: String
        - name: String
        + addBook(book: Book): void
        + removeBook(book: Book): void
        + issueBook(book: Book, member: Member): void
        + collectFine(member: Member, amount: Double): void
    }

    class Transaction {
        - transactionID: String
        - book: Book
        - member: Member
        - issueDate: Date
        - returnDate: Date
        - fine: Fine
        + calculateFine(): Double
        + closeTransaction(): void
    }

    class Fine {
        - fineID: String
        - member: Member
        - amount: Double
        - paymentStatus: Boolean
        + calculateFine(dueDate: Date, returnDate: Date): Double
        + payFine(amount: Double): void
    }

    Book <|-- PrintedBook
    Book <|-- EBook
    Library "1" -- "many" Book : contains
    Library "1" -- "many" Member : manages
    Library "1" -- "many" Librarian : employs
    Member "1" -- "many" Book : borrows
    Librarian "1" -- "many" Book : manages
    Librarian "1" -- "many" Transaction : records
    Transaction "1" -- "1" Fine : calculates
