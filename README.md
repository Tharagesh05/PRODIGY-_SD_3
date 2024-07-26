To develop a program that allows users to store and manage contact information, you can use a programming language like Python. Here's a basic outline of how you can structure the program:

1. **Data Structure**: Use a list of dictionaries to store contact information. Each dictionary will represent a contact with keys like "name," "phone number," and "email."

2. **Functions**:
   - `add_contact()`: Add a new contact by entering their name, phone number, and email address.
   - `view_contacts()`: Display the list of all contacts.
   - `edit_contact()`: Modify the details of an existing contact.
   - `delete_contact()`: Remove a contact from the list.
   - `save_contacts()`: Save the contact list to a file for persistent storage.
   - `load_contacts()`: Load the contact list from a file.

3. **Persistent Storage**: Use a file (e.g., JSON) to store contact information. This allows the data to persist between sessions.

Here is a simple implementation in Python:

```python
import json

# File to store contacts
FILE_NAME = "contacts.json"

# Function to load contacts from the file
def load_contacts():
    try:
        with open(FILE_NAME, "r") as file:
            return json.load(file)
    except FileNotFoundError:
        return []

# Function to save contacts to the file
def save_contacts(contacts):
    with open(FILE_NAME, "w") as file:
        json.dump(contacts, file)

# Function to add a new contact
def add_contact(contacts):
    name = input("Enter name: ")
    phone = input("Enter phone number: ")
    email = input("Enter email: ")
    contacts.append({"name": name, "phone": phone, "email": email})
    save_contacts(contacts)

# Function to view all contacts
def view_contacts(contacts):
    for contact in contacts:
        print(f"Name: {contact['name']}, Phone: {contact['phone']}, Email: {contact['email']}")

# Function to edit a contact
def edit_contact(contacts):
    name = input("Enter the name of the contact to edit: ")
    for contact in contacts:
        if contact['name'] == name:
            contact['phone'] = input("Enter new phone number: ")
            contact['email'] = input("Enter new email: ")
            save_contacts(contacts)
            return
    print("Contact not found")

# Function to delete a contact
def delete_contact(contacts):
    name = input("Enter the name of the contact to delete: ")
    for contact in contacts:
        if contact['name'] == name:
            contacts.remove(contact)
            save_contacts(contacts)
            return
    print("Contact not found")

# Main function to run the program
def main():
    contacts = load_contacts()
    while True:
        print("\n1. Add Contact\n2. View Contacts\n3. Edit Contact\n4. Delete Contact\n5. Exit")
        choice = input("Choose an option: ")
        if choice == "1":
            add_contact(contacts)
        elif choice == "2":
            view_contacts(contacts)
        elif choice == "3":
            edit_contact(contacts)
        elif choice == "4":
            delete_contact(contacts)
        elif choice == "5":
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
```

This program:
- Uses a list of dictionaries to store contacts.
- Provides functions to add, view, edit, and delete contacts.
- Uses JSON for file storage to maintain contact information persistently.

You can run this program, and it will prompt you for the necessary actions to manage the contacts.
