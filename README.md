# Organic-fruits-store
Organic fruits and food availble in online
import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { ShoppingCart } from "lucide-react";

const fruits = [
  { id: 1, name: "Organic Apple", price: 2.5, image: "https://via.placeholder.com/150" },
  { id: 2, name: "Organic Banana", price: 1.2, image: "https://via.placeholder.com/150" },
  { id: 3, name: "Organic Orange", price: 2.0, image: "https://via.placeholder.com/150" }
];

export default function OrganicFruitsApp() {
  const [cart, setCart] = useState([]);
  const [checkout, setCheckout] = useState(false);

  const addToCart = (fruit) => {
    setCart([...cart, fruit]);
  };

  const handleCheckout = () => {
    setCheckout(true);
  };

  return (
    <div className="p-8 bg-green-100 min-h-screen">
      <h1 className="text-3xl font-bold text-center mb-6">Organic Fruits Store 🍏</h1>
      <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
        {fruits.map((fruit) => (
          <Card key={fruit.id} className="p-4 shadow-md rounded-lg">
            <img src={fruit.image} alt={fruit.name} className="w-full h-40 object-cover rounded-md" />
            <CardContent className="mt-4 text-center">
              <h2 className="text-xl font-semibold">{fruit.name}</h2>
              <p className="text-gray-600">${fruit.price.toFixed(2)}</p>
              <Button className="mt-2" onClick={() => addToCart(fruit)}>Add to Cart</Button>
            </CardContent>
          </Card>
        ))}
      </div>
      <div className="mt-8 p-4 bg-white shadow-md rounded-lg">
        <h2 className="text-2xl font-bold">Shopping Cart <ShoppingCart className="inline" /></h2>
        {cart.length > 0 ? (
          <>
            {cart.map((item, index) => (
              <p key={index} className="text-lg">{item.name} - ${item.price.toFixed(2)}</p>
            ))}
            <Button className="mt-4" onClick={handleCheckout}>Proceed to Checkout</Button>
          </>
        ) : (
          <p className="text-gray-500">Cart is empty</p>
        )}
      </div>
      {checkout && (
        <div className="fixed inset-0 bg-gray-900 bg-opacity-50 flex justify-center items-center">
          <div className="bg-white p-6 rounded-lg shadow-lg text-center">
            <h2 className="text-2xl font-bold">Checkout</h2>
            <p className="text-lg">Total: ${cart.reduce((acc, item) => acc + item.price, 0).toFixed(2)}</p>
            <Button className="mt-4" onClick={() => alert('Payment Successful!')}>Pay Now</Button>
            <Button className="mt-2" variant="outline" onClick={() => setCheckout(false)}>Cancel</Button>
          </div>
        </div>
      )}
    </div>
  );
}
