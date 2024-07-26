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


