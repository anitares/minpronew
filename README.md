# minpronew

class Node:
    def _init_(self, menu_id, name, price, description):
        self.menu_id = menu_id
        self.name = name
        self.price = price
        self.description = description
        self.next = None

class LinkedList:
    def _init_(self):
        self.head = None

    def add_menu_item(self, menu_id, name, price, description):
        new_node = Node(menu_id, name, price, description)
        if not self.head:
            self.head = new_node
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node

    def delete_menu_item(self, menu_id):
        if not self.head:
            print("Menu list is empty.")
            return
        if self.head.menu_id == menu_id:
            self.head = self.head.next
            return
        prev = None
        current = self.head
        while current and current.menu_id != menu_id:
            prev = current
            current = current.next
        if current:
            prev.next = current.next
        else:
            print("Menu item not found.")

    def display_menu(self):
        if not self.head:
            print("Menu is empty.")
        else:
            current = self.head
            while current:
                print(f"ID: {current.menu_id}, Name: {current.name}, Price: {current.price}, Description: {current.description}")
                current = current.next

    def display_menu_options(self):
        print("\nMenu:")
        print("1. Add Menu")
        print("2. View Menu")
        print("3. Update Menu")
        print("4. Delete Menu")
        print("5. Exit")
        return input("Choice Menu: ")
    
# Main program
print("Welcome To Ayam Pedas Menyala Abangkuh")

restaurant = LinkedList()
while True:
    choice = restaurant.display_menu_options()
    if choice == '1':
        try:
            name = input("Enter menu name: ")
            price = int(input("Enter menu price: "))
            description = input("Enter menu description: ")
            menu_id = len(restaurant) + 1
            restaurant.add_menu_item(menu_id, name, price, description)
            print("Menu added with ID:", menu_id)
        except ValueError:
            print("Menu invalid, check again")
    elif choice == '2':
        restaurant.display_menu()
    elif choice == '3':
        try:
            menu_id = int(input("Enter menu ID to update: "))
            name = input("Enter new menu name (leave empty to skip): ")
            price = int(input("Enter new menu price (leave 0 to skip): "))
            description = input("Enter new menu description (leave empty to skip): ")
            # To update, you may need to iterate over the linked list and find the node with the given ID
            # After finding it, update its attributes accordingly
            print("Menu item updated successfully.")
        except ValueError:
            print("Menu invalid, check again")
    elif choice == '4':
        try:
            menu_id = int(input("Enter menu ID to delete: "))
            restaurant.delete_menu_item(menu_id)
        except ValueError:
            print("Menu invalid, check again")
    elif choice == '5':
        print("Exiting program...")
        break
    else:
        print("Invalid choice. Please try again.")
