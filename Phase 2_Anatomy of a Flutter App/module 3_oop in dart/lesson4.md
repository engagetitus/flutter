
# Lesson 4: Practical OOP with Dart

- **Overview**: Hands-on practice with OOP concepts in Dart.
- **Key Concepts**:
  - Building a Simple Application 📱
  - Using Classes and Objects 🛠️
  - Implementing OOP Principles 🧩

# Building a Simple Application 📱

- Create a simple console application that models a library system.

# Using Classes and Objects 🛠️

- Define classes for `Book`, `Library`, and `Member`.

  ```dart
  class Book {
    String title;
    String author;

    Book(this.title, this.author);

    void details() {
      print('Title: $title, Author: $author');
    }
  }

  class Library {
    List<Book> books = [];

    void addBook(Book book) {
      books.add(book);
    }

    void showBooks() {
      for (var book in books) {
        book.details();
      }
    }
  }

  class Member {
    String name;

    Member(this.name);

    void borrowBook(Book book) {
      print('$name borrowed "${book.title}" by ${book.author}');
    }
  }

  void main() {
    var library = Library();
    var book1 = Book('1984', 'George Orwell');
    var book2 = Book('Brave New World', 'Aldous Huxley');

    library.addBook(book1);
    library.addBook(book2);

    var member = Member('Alice');
    member.borrowBook(book1);

    library.showBooks();
  }
