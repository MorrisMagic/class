class Product {
    constructor(id, name, price) {
        this.id = id;
        this.name = name;
        this.price = price;
    }
}

class ShoppingCartItem {
    constructor(product, quantity) {
        this.product = product;
        this.quantity = quantity;
    }

    totalPrice() {
        return this.product.price * this.quantity;
    }
}

class ShoppingCart {
    constructor() {
        this.items = [];
    }

    addItem(product, quantity) {
        const existingItem = this.items.find(item => item.product.id === product.id);
        if (existingItem) {
            existingItem.quantity += quantity;
        } else {
            const newItem = new ShoppingCartItem(product, quantity);
            this.items.push(newItem);
        }
    }

    removeItem(productId) {
        this.items = this.items.filter(item => item.product.id !== productId);
    }

    getTotal() {
        return this.items.reduce((total, item) => total + item.totalPrice(), 0);
    }

    displayItems() {
        if (this.items.length === 0) {
            console.log("Your cart is empty.");
            return;
        }
        console.log("Shopping Cart Items:");
        this.items.forEach(item => {
            console.log(`${item.product.name} - Quantity: ${item.quantity}, Total Price: $${item.totalPrice().toFixed(2)}`);
        });
    }
}

const product1 = new Product(1, 'Apple', 0.99);
const product2 = new Product(2, 'Banana', 0.79);
const product3 = new Product(3, 'Orange', 0.89);

const cart = new ShoppingCart();

cart.addItem(product1, 3);
cart.addItem(product2, 2);
cart.addItem(product3, 5);

cart.displayItems();
console.log(`Total Price: $${cart.getTotal().toFixed(2)}`);

cart.removeItem(2);

cart.displayItems();
console.log(`Total Price: $${cart.getTotal().toFixed(2)}`);
