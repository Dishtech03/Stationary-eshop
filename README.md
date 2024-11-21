# Stationary-eshop
import React, { useState } from 'react';

const LoginForm = () => {
  const [role, setRole] = useState('customer');
  const [credentials, setCredentials] = useState({ email: '', password: '' });

  const handleLogin = () => {
    if (role === 'customer') {
      // Redirect to customer dashboard
      window.location.href = '/customer/dashboard';
    } else {
      // Redirect to seller dashboard
      window.location.href = '/seller/dashboard';
    }
  };

  return (
    <div className="p-4 max-w-md mx-auto">
      <h2 className="text-xl font-bold mb-4">Login</h2>
      <div className="mb-4">
        <label className="block mb-2">Select Role:</label>
        <select
          value={role}
          onChange={(e) => setRole(e.target.value)}
          className="border p-2 w-full"
        >
          <option value="customer">Customer</option>
          <option value="seller">Seller</option>
        </select>
      </div>
      <div className="mb-4">
        <label className="block mb-2">Email:</label>
        <input
          type="email"
          value={credentials.email}
          onChange={(e) => setCredentials({ ...credentials, email: e.target.value })}
          className="border p-2 w-full"
        />
      </div>
      <div className="mb-4">
        <label className="block mb-2">Password:</label>
        <input
          type="password"
          value={credentials.password}
          onChange={(e) => setCredentials({ ...credentials, password: e.target.value })}
          className="border p-2 w-full"
        />
      </div>
      <button onClick={handleLogin} className="bg-blue-500 text-white p-2 w-full">
        Login
      </button>
    </div>
  );
};

export default LoginForm;
import React from 'react';

const CustomerDashboard = () => {
  return (
    <div className="p-4">
      <h2 className="text-2xl font-bold">Welcome to Customer Dashboard</h2>
      <p>Browse and shop from your favorite stationery stores!</p>
    </div>
  );
};

export default CustomerDashboard;
import React from 'react';

const SellerDashboard = () => {
  return (
    <div className="p-4">
      <h2 className="text-2xl font-bold">Seller Dashboard</h2>
      <p>Manage your shop, products, and orders here.</p>
    </div>
  );
};

export default SellerDashboard;
import React from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import LoginForm from './components/LoginForm';
import CustomerDashboard from './components/CustomerDashboard';
import SellerDashboard from './components/SellerDashboard';

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<LoginForm />} />
        <Route path="/customer/dashboard" element={<CustomerDashboard />} />
        <Route path="/seller/dashboard" element={<SellerDashboard />} />
      </Routes>
    </Router>
  );
};

export default App;
import React, { useState } from 'react';

const ProductManagementPage = () => {
  const [products, setProducts] = useState([
    { id: 1, name: 'Notebook', price: 50 },
    { id: 2, name: 'Pen', price: 10 },
  ]);

  const addProduct = () => {
    const newProduct = { id: products.length + 1, name: 'New Product', price: 0 };
    setProducts([...products, newProduct]);
  };

  return (
    <div className="p-4">
      <h2 className="text-xl font-bold">Manage Products</h2>
      <ul>
        {products.map((product) => (
          <li key={product.id}>
            {product.name} - ₹{product.price}
          </li>
        ))}
      </ul>
      <button onClick={addProduct} className="bg-green-500 text-white p-2 mt-4">
        Add Product
      </button>
    </div>
  );
};

export default ProductManagementPage;
import React from 'react';

const OrderManagementPage = () => {
  const orders = [
    { id: 1, customer: 'John Doe', product: 'Notebook', quantity: 2 },
    { id: 2, customer: 'Jane Doe', product: 'Pen', quantity: 5 },
  ];

  return (
    <div className="p-4">
      <h2 className="text-xl font-bold">Manage Orders</h2>
      <table className="table-auto w-full">
        <thead>
          <tr>
            <th>ID</th>
            <th>Customer</th>
            <th>Product</th>
            <th>Quantity</th>
          </tr>
        </thead>
        <tbody>
          {orders.map((order) => (
            <tr key={order.id}>
              <td>{order.id}</td>
              <td>{order.customer}</td>
              <td>{order.product}</td>
              <td>{order.quantity}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};

export default OrderManagementPage;
