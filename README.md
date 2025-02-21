# 🛒 Web Shop - React & Context API

## 📚 Overview

**Web Shop** is a modern e-commerce application built with **React**, utilizing the **Context API** for state management. This project features a dynamic shopping cart, a product listing page, and a modal-based checkout system. The app is optimized for **performance, scalability, and maintainability** using **Vite** for fast development.

---

## 🚀 Features

- **Dynamic Shopping Cart** - Add and update items in real time.
- **Context API for State Management** - Efficient and scalable global state handling.
- **Reusable Components** - Modular structure for scalability.
- **Fast Development with Vite** - Lightning-fast development environment.
- **React Hooks (`useReducer`, `useContext`, `useRef`)** - State management and component logic.
- **Modal-Based Cart Checkout** - Smooth user experience with dialogs.
- **Formatted Pricing** - Ensures clean and readable currency display.

---

## 💻 Technologies Used

- **React** - Frontend framework for UI development.
- **Context API & Reducer** - Efficient state management.
- **Vite** - Fast development and build tool.
- **JavaScript (ES6+)** - Modern syntax and best practices.
- **JSX** - Component-based UI rendering.
- **CSS** - Basic styling for responsiveness.

---

## 📸 Project Preview

![image](https://github.com/user-attachments/assets/3ffb303b-e71e-4b51-92ca-48729eb4879a)
![image](https://github.com/user-attachments/assets/2afe787d-75f8-492a-8e98-64df8079e0e1)


---

## 📂 Project Structure

```
web-shop/
├── src/
│   ├── assets/                   # Static assets (images, icons)
│   ├── components/               # UI Components
│   │   ├── Cart.jsx              # Shopping cart component
│   │   ├── CartModal.jsx         # Modal for checkout
│   │   ├── Header.jsx            # Navigation header
│   │   ├── Product.jsx           # Product card component
│   │   ├── Shop.jsx              # Product listing page
│   ├── store/
│   │   ├── shopping-cart-context.jsx  # Context API for cart management
│   ├── dummy-products.js         # Sample product data
│   ├── App.jsx                   # Main application component
│   ├── main.jsx                  # Entry point of the app
│   ├── index.css                 # Global styles
├── public/                       # Static files (index.html)
├── package.json                  # Project dependencies and scripts
├── vite.config.js                 # Vite configuration
├── README.md                      # Project documentation
```

---

## 💾 Installation & Setup

### 1️⃣ Clone the Repository

```sh
git clone https://github.com/Caiko/web-shop.git
cd web-shop
```

### 2️⃣ Install Dependencies

```sh
npm install
```

### 3️⃣ Start the Development Server

```sh
npm run dev
```

Then open [**localhost:5173**](http://localhost:5173) (default for Vite) in your browser.

---

## ⚙️ Usage

### **1. Adding Items to Cart**
- Click **"Add to Cart"** on any product.
- The cart counter in the **Header** updates in real time.

### **2. Managing Cart Items**
- Open the cart modal by clicking the **Cart button**.
- Increase or decrease item quantity using the `+` and `-` buttons.
- Items are removed if quantity reaches `0`.

### **3. Checkout Process**
- Click **Checkout** inside the cart modal.
- Simulates a real checkout process.

---

## 🎯 Features Breakdown

### **1. Context API for Global State Management**
```jsx
export const CartContext = createContext({
  items: [],
  addItemsToCart: () => {},
  updateItemQuantity: () => {},
});
```
- Manages cart state globally.
- Prevents prop drilling issues.

### **2. Reducer for Cart Actions**
```jsx
function shoppingCartReducer(state, action) {
  if (action.type === "ADD_ITEM") {
    const updatedItems = [...state.items];
    const existingCartItemIndex = updatedItems.findIndex(
      (cartItem) => cartItem.id === action.payload
    );
    
    if (existingCartItemIndex >= 0) {
      updatedItems[existingCartItemIndex].quantity += 1;
    } else {
      const product = DUMMY_PRODUCTS.find(
        (product) => product.id === action.payload
      );
      updatedItems.push({ ...product, quantity: 1 });
    }
    
    return { ...state, items: updatedItems };
  }
  return state;
}
```
- Handles **adding items** and **updating quantities** efficiently.

### **3. Dynamic Cart UI**
```jsx
{items.length > 0 && (
  <ul id="cart-items">
    {items.map((item) => (
      <li key={item.id}>
        <span>{item.name} (${item.price})</span>
        <button onClick={() => updateItemQuantity(item.id, -1)}>-</button>
        <span>{item.quantity}</span>
        <button onClick={() => updateItemQuantity(item.id, 1)}>+</button>
      </li>
    ))}
  </ul>
)}
```
- Updates in real time when items are added or removed.
- Uses **React Context** to manage changes efficiently.

### **4. Modal-Based Checkout System**
```jsx
const modal = useRef();
function handleOpenCartClick() {
  modal.current.open();
}
```
- Uses `useRef()` to open and close the cart modal.
- Enhances **user experience** with smooth interactions.


