# Order<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Krishika Fresh Farm - Shop</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #2d6a4f;
            --secondary: #74c69d;
            --accent: #ff7b00;
            --light: #f8f9fa;
            --dark: #1b4332;
            --white: #ffffff;
            --shadow: 0 4px 12px rgba(0,0,0,0.08);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }

        body {
            font-family: 'Outfit', sans-serif;
            background-color: var(--light);
            color: var(--dark);
            line-height: 1.6;
        }

        /* Header */
        header {
            background: var(--white);
            padding: 20px;
            text-align: center;
            box-shadow: var(--shadow);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .shop-name { color: var(--primary); font-size: 1.5rem; font-weight: 700; margin-bottom: 4px; }
        .tagline { font-size: 0.85rem; color: #666; max-width: 300px; margin: 0 auto; }

        /* Filters */
        .categories {
            display: flex;
            gap: 10px;
            overflow-x: auto;
            padding: 15px;
            scrollbar-width: none;
        }
        .categories::-webkit-scrollbar { display: none; }
        
        .cat-btn {
            background: var(--white);
            border: 1px solid var(--secondary);
            padding: 8px 18px;
            border-radius: 20px;
            white-space: nowrap;
            font-size: 0.9rem;
            cursor: pointer;
            transition: 0.3s;
        }
        .cat-btn.active { background: var(--primary); color: var(--white); border-color: var(--primary); }

        /* Product Grid */
        .product-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
            gap: 15px;
            padding: 15px;
        }

        .product-card {
            background: var(--white);
            border-radius: 12px;
            overflow: hidden;
            box-shadow: var(--shadow);
            display: flex;
            flex-direction: column;
        }

        .product-img {
            width: 100%;
            height: 150px;
            object-fit: cover;
            background: #eee;
        }

        .product-info { padding: 12px; flex-grow: 1; display: flex; flex-direction: column; }
        .p-name { font-weight: 600; font-size: 0.95rem; margin-bottom: 4px; }
        .p-desc { font-size: 0.75rem; color: #777; margin-bottom: 8px; flex-grow: 1; }
        .p-price { font-weight: 700; color: var(--primary); font-size: 1.1rem; margin-bottom: 10px; }

        .add-btn {
            background: var(--primary);
            color: var(--white);
            border: none;
            padding: 10px;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: transform 0.1s;
        }
        .add-btn:active { transform: scale(0.95); }

        /* Cart UI */
        .cart-trigger {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: var(--accent);
            color: var(--white);
            width: 60px;
            height: 60px;
            border-radius: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 20px rgba(255,123,0,0.4);
            cursor: pointer;
            z-index: 99;
        }

        .cart-count {
            position: absolute;
            top: 0;
            right: 0;
            background: var(--dark);
            font-size: 12px;
            padding: 4px 8px;
            border-radius: 10px;
        }

        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            display: none;
            z-index: 1000;
            justify-content: flex-end;
        }

        .modal-content {
            background: var(--white);
            width: 100%;
            max-width: 500px;
            height: 100%;
            padding: 20px;
            overflow-y: auto;
            animation: slideIn 0.3s ease-out;
        }

        @keyframes slideIn { from { transform: translateX(100%); } to { transform: translateX(0); } }

        .cart-item {
            display: flex;
            align-items: center;
            gap: 15px;
            padding: 15px 0;
            border-bottom: 1px solid #eee;
        }

        .qty-controls { display: flex; align-items: center; gap: 10px; margin-top: 5px; }
        .qty-btn { width: 28px; height: 28px; border-radius: 14px; border: 1px solid #ddd; background: none; font-size: 18px; cursor: pointer; }

        /* Form Styling */
        .checkout-form { margin-top: 20px; display: none; }
        .form-group { margin-bottom: 15px; }
        label { display: block; font-size: 0.9rem; margin-bottom: 5px; font-weight: 600; }
        input, textarea { width: 100%; padding: 12px; border: 1px solid #ddd; border-radius: 8px; font-family: inherit; }

        .btn-block { width: 100%; padding: 15px; border-radius: 8px; border: none; font-weight: 700; font-size: 1rem; cursor: pointer; margin-top: 10px; }
        .btn-order { background: var(--primary); color: white; }
        .btn-close { background: #eee; color: #333; margin-top: 5px; }

        /* WhatsApp Button */
        .wa-float {
            position: fixed;
            bottom: 20px;
            left: 20px;
            background: #25d366;
            color: white;
            padding: 10px 15px;
            border-radius: 50px;
            text-decoration: none;
            font-size: 14px;
            display: flex;
            align-items: center;
            gap: 8px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            z-index: 98;
        }

        @media (min-width: 768px) {
            .product-grid { grid-template-columns: repeat(4, 1fr); padding: 40px; }
        }
    </style>
</head>
<body>

<header>
    <div class="shop-name">Krishika Fresh Farm</div>
    <div class="tagline">Cake, Ragi Laddu, Makhana & Millet Cookies delivered to your door</div>
</header>

<div class="categories" id="cat-filters">
    <button class="cat-btn active" onclick="filterProducts('All')">All</button>
    <button class="cat-btn" onclick="filterProducts('Sweets')">Sweets</button>
    <button class="cat-btn" onclick="filterProducts('Makhana')">Makhana</button>
    <button class="cat-btn" onclick="filterProducts('Cookies')">Cookies & Snacks</button>
</div>

<div class="product-grid" id="product-container">
    </div>

<div class="cart-trigger" onclick="toggleCart()">
    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"/></svg>
    <span class="cart-count" id="cart-count">0</span>
</div>

<a href="https://wa.me/917319656552" class="wa-float" target="_blank">
    <svg width="20" height="20" fill="currentColor" viewBox="0 0 24 24"><path d="M.057 24l1.687-6.163c-1.041-1.804-1.588-3.849-1.587-5.946.003-6.556 5.338-11.891 11.893-11.891 3.181.001 6.167 1.24 8.413 3.488 2.245 2.248 3.481 5.236 3.48 8.414-.003 6.557-5.338 11.892-11.893 11.892-1.99-.001-3.951-.5-5.688-1.448l-6.305 1.654zm6.597-3.807c1.676.995 3.276 1.591 5.3 1.592 5.548 0 10.061-4.512 10.063-10.062 0-2.69-1.048-5.216-2.953-7.124s-4.439-2.952-7.128-2.952c-5.55 0-10.061 4.511-10.064 10.061 0 2.132.58 3.64 1.61 5.421l-.994 3.63 3.73-.978z"/></svg>
    Chat with us
</a>

<div class="modal" id="cart-modal">
    <div class="modal-content">
        <h2 style="margin-bottom: 20px;">Your Basket</h2>
        <div id="cart-items-list">
            </div>

        <div id="cart-summary" style="margin-top: 20px;">
            <div style="display: flex; justify-content: space-between; font-weight: 700; font-size: 1.2rem;">
                <span>Total:</span>
                <span id="grand-total">₹0</span>
            </div>
            
            <button class="btn-block btn-order" id="checkout-start-btn" onclick="showCheckoutForm()">Proceed to Checkout</button>
            
            <form id="order-form" class="checkout-form" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
                <input type="hidden" name="_subject" value="New Order - Krishika Fresh Farm">
                <textarea name="Order_Details" id="hidden-order-details" style="display:none;"></textarea>
                
                <div class="form-group">
                    <label>Full Name *</label>
                    <input type="text" name="Customer_Name" required placeholder="John Doe">
                </div>
                <div class="form-group">
                    <label>Phone Number *</label>
                    <input type="tel" name="Phone" required placeholder="+91 00000 00000">
                </div>
                <div class="form-group">
                    <label>Delivery Address *</label>
                    <textarea name="Address" required rows="3" placeholder="Street, Area, Pincode"></textarea>
                </div>
                <div class="form-group">
                    <label>Instructions (Optional)</label>
                    <input type="text" name="Note" placeholder="e.g. Leave at gate">
                </div>
                
                <button type="submit" class="btn-block btn-order">Place Order</button>
            </form>

            <button class="btn-block btn-close" onclick="toggleCart()">Close</button>
        </div>
    </div>
</div>

<script>
    // CONFIGURATION
    const FORMSPREE_ID = "YOUR_FORM_ID"; // <--- REPLACE THIS
    const products = [
        { id: 1, name: "Ragi Laddu (400g)", price: 342, cat: "Sweets", img: "https://i.ibb.co/gZbnYc9J/Screenshot-2026-04-28-17-07-17-782-com-meesho-supply.jpg", desc: "Nutritious and delicious handmade Ragi balls." },
        { id: 2, name: "Minty-Pudina Makhana", price: 180, cat: "Makhana", img: "https://i.ibb.co/LhY0m2H/makhana.jpg", desc: "Refreshing mint-flavored roasted foxnuts." },
        { id
