# BCA__python_assignment_2
"""
Name: Tanmay Balyan
Roll No.:2501060023
Serial No.:4
Date: 19 Nov 2025
Project: Library Management System
"""

# -------------------------------
# Global Data Stores
# -------------------------------
books = {}
borrowed = {}

# -------------------------------
# Function: Display Menu
# -------------------------------
def display_menu():
    print("\n" + "="*40)
    print("📚 LIBRARY MANAGEMENT SYSTEM")
    print("="*40)
    print("1. Add Book")
    print("2. View Books")
    print("3. Search Book")
    print("4. Borrow Book")
    print("5. Return Book")
    print("6. Exit")
    print("="*40)

# -------------------------------
# Task 2: Add Book
# -------------------------------
def add_books():
    print("\n--- Add New Books ---")
    for i in range(5):  # At least 5 books
        print(f"\nEntering book {i+1}:")
        book_id = input("Enter Book ID: ")
        title = input("Enter Title: ")
        author = input("Enter Author: ")
        copies = int(input("Enter Number of Copies: "))

        books[book_id] = {
            "title": title,
            "author": author,
            "copies": copies
        }
    print("\n✔ 5 Books Added Successfully!")

# -------------------------------
# Task 3: View Books
# -------------------------------
def view_books():
    print("\n--- Book List ---")
    print(f"{'ID':<10}{'Title':<25}{'Author':<20}{'Copies':<10}")
    print("-"*65)

    for bid, info in books.items():
        print(f"{bid:<10}{info['title']:<25}{info['author']:<20}{info['copies']:<10}")

# -------------------------------
# Search Functions
# -------------------------------
def search_by_id(book_id):
    return books.get(book_id, None)

def search_by_title(keyword):
    # substring search
    results = {bid: info for bid, info in books.items()
               if keyword.lower() in info["title"].lower()}
    return results

def search_books():
    print("\n--- Search Book ---")
    print("1. By Book ID")
    print("2. By Title")
    choice = input("Enter choice: ")

    if choice == "1":
        bid = input("Enter Book ID: ")
        result = search_by_id(bid)
        if result:
            print("\n✔ Book Found:")
            print(result)
        else:
            print("❌ Book Not Found")

    elif choice == "2":
        title = input("Enter Title Keyword: ")
        results = search_by_title(title)
        if results:
            print("\n✔ Books Matching Search:")
            for bid, info in results.items():
                print(f"{bid}: {info}")
        else:
            print("❌ No Books Found")

# -------------------------------
# Task 4: Borrow Book
# -------------------------------
def borrow_book():
    print("\n--- Borrow Book ---")
    student = input("Enter Student Name: ")
    bid = input("Enter Book ID: ")

    if bid not in books:
        print("❌ Book does not exist!")
        return

    if books[bid]["copies"] > 0:
        books[bid]["copies"] -= 1
        borrowed[student] = bid
        print(f"✔ {student} borrowed {bid} successfully!")
    else:
        print("❌ No copies left!")

# -------------------------------
# Task 5: Return Book
# -------------------------------
def return_book():
    print("\n--- Return Book ---")
    student = input("Enter Student Name: ")
    bid = input("Enter Book ID: ")

    if student in borrowed and borrowed[student] == bid:
        books[bid]["copies"] += 1
        del borrowed[student]
        print("✔ Book Returned Successfully!")
    else:
        print("❌ No such borrowing record!")

    # List comprehension for borrowed books
    borrowed_list = [f"{s} -> {b}" for s, b in borrowed.items()]
    print("\nCurrent Borrowed Books:")
    print(borrowed_list)

# -------------------------------
# Task 6: Loop + Exit
# -------------------------------
def main():
    while True:
        display_menu()
        choice = input("Enter your choice (1-6): ")

        if choice == "1":
            add_books()
        elif choice == "2":
            view_books()
        elif choice == "3":
            search_books()
        elif choice == "4":
            borrow_book()
        elif choice == "5":
            return_book()
        elif choice == "6":
            print("\n📘 Exiting Program... Goodbye!\n")
            break
        else:
            print("❌ Invalid choice, try again.")
