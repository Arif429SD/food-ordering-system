# food-ordering-systemimport java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class FoodItem {
    private String name;
    private double price;

    public FoodItem(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }
}

class Order {
    private List<FoodItem> items;

    public Order() {
        items = new ArrayList<>();
    }

    public void addItem(FoodItem item) {
        items.add(item);
    }

    public List<FoodItem> getItems() {
        return items;
    }

    public double getTotalPrice() {
        double totalPrice = 0;
        for (FoodItem item : items) {
            totalPrice += item.getPrice();
        }
        return totalPrice;
    }
}

class Menu {
    private List<FoodItem> items;

    public Menu() {
        items = new ArrayList<>();
    }

    public void addItem(FoodItem item) {
        items.add(item);
    }

    public List<FoodItem> getItems() {
        return items;
    }
}

class Customer {
    private String name;
    private String address;
    private String contactInfo;

    public Customer(String name, String address, String contactInfo) {
        this.name = name;
        this.address = address;
        this.contactInfo = contactInfo;
    }

    public String getName() {
        return name;
    }

    public String getAddress() {
        return address;
    }

    public String getContactInfo() {
        return contactInfo;
    }
}

public class FoodOrderingSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Create a menu
        Menu menu = new Menu();
        while (true) {
            System.out.println("Enter food name (type 'done' to finish adding food items): ");
            String foodName = scanner.nextLine();
            if (foodName.equalsIgnoreCase("done")) {
                break;
            }
            System.out.println("Enter price for " + foodName + ": ");
            double price = scanner.nextDouble();
            scanner.nextLine(); // consume newline
            menu.addItem(new FoodItem(foodName, price));
        }

        // Create a customer
        System.out.println("Enter customer name: ");
        String customerName = scanner.nextLine();
        System.out.println("Enter customer address: ");
        String address = scanner.nextLine();
        System.out.println("Enter customer contact info: ");
        String contactInfo = scanner.nextLine();
        Customer customer = new Customer(customerName, address, contactInfo);

        // Create an order
        Order order = new Order();
        while (true) {
            System.out.println("Enter food item to order (type 'done' to finish ordering): ");
            String foodToOrder = scanner.nextLine();
            if (foodToOrder.equalsIgnoreCase("done")) {
                break;
            }
            // Search for the food item in the menu
            boolean found = false;
            for (FoodItem item : menu.getItems()) {
                if (item.getName().equalsIgnoreCase(foodToOrder)) {
                    order.addItem(item);
                    found = true;
                    break;
                }
            }
            if (!found) {
                System.out.println("Sorry, " + foodToOrder + " is not available in the menu.");
            }
        }

        // Display order summary
        System.out.println("Order Summary for " + customer.getName() + ":");
        for (FoodItem item : order.getItems()) {
            System.out.println(item.getName() + "  - " + item.getPrice() + " taka");
        }
        System.out.println("Total: " + order.getTotalPrice() + " taka");

        scanner.close();
    }
}
