<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hotel Bhondawe Palace - Digital Experience</title>
    <style>
        :root {
            --primary-gold: #D4AF37;
            --primary-dark: #1a1a1a;
            --bg-light: #f9f9f9;
            --text-grey: #555;
            --veg-green: #008000;
            --nonveg-red: #A52A2A;
            --google-blue: #4285F4;
        }

        * {
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            margin: 0;
            padding: 0;
            background-color: #eee;
            color: var(--primary-dark);
            /* Mobile wrapper simulation */
            display: flex;
            justify-content: center;
        }

        /* Mobile Container */
        #app-container {
            width: 100%;
            max-width: 480px;
            background-color: white;
            min-height: 100vh;
            position: relative;
            padding-bottom: 80px; /* Space for footer */
            box-shadow: 0 0 20px rgba(0,0,0,0.1);
        }

        /* --- HEADER --- */
        header {
            background-color: var(--primary-dark);
            color: var(--primary-gold);
            text-align: center;
            padding: 20px 15px;
            border-bottom: 3px solid var(--primary-gold);
        }

        .logo-area img {
            max-height: 80px;
            width: auto;
            display: block;
            margin: 0 auto 10px auto;
        }

        .hotel-name {
            font-size: 1.2rem;
            font-weight: 700;
            letter-spacing: 1px;
            text-transform: uppercase;
        }

        /* --- PAGES --- */
        .page {
            display: none; /* Hidden by default */
            padding: 20px;
            animation: fadeIn 0.3s ease;
        }

        .page.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* --- LANDING PAGE BUTTONS --- */
        .landing-btn {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100%;
            padding: 25px;
            margin-bottom: 15px;
            background: white;
            border: 1px solid #ddd;
            border-left: 5px solid var(--primary-gold);
            border-radius: 8px;
            font-size: 1.2rem;
            font-weight: 600;
            color: var(--primary-dark);
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            cursor: pointer;
            transition: transform 0.1s;
        }

        .landing-btn:active {
            transform: scale(0.98);
            background-color: #f0f0f0;
        }

        /* --- BACK BUTTON --- */
        .back-btn {
            background: none;
            border: none;
            color: var(--primary-dark);
            font-size: 1rem;
            font-weight: 600;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            cursor: pointer;
        }
        .back-btn::before {
            content: '←';
            font-size: 1.5rem;
            margin-right: 8px;
        }

        /* --- MENU STYLES --- */
        .menu-section-title {
            font-size: 1.3rem;
            color: var(--primary-gold);
            background-color: var(--primary-dark);
            padding: 10px 15px;
            margin: 25px -20px 15px -20px; /* Full width */
            text-align: center;
            font-weight: 700;
        }

        .menu-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0;
            border-bottom: 1px solid #eee;
        }

        .item-details {
            flex: 1;
        }

        .item-header {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .item-name {
            font-weight: 600;
            font-size: 1.05rem;
        }

        .item-desc {
            font-size: 0.85rem;
            color: #777;
            margin-top: 4px;
        }

        .item-price {
            font-weight: 700;
            color: var(--primary-dark);
            margin-top: 4px;
        }

        /* Icons */
        .icon-veg, .icon-nonveg {
            width: 16px;
            height: 16px;
            border-radius: 3px;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
            border: 2px solid;
            font-size: 10px;
        }
        .icon-veg { border-color: var(--veg-green); color: var(--veg-green); }
        .icon-veg::after { content: '●'; font-size: 12px; }
        
        .icon-nonveg { border-color: var(--nonveg-red); color: var(--nonveg-red); }
        .icon-nonveg::after { content: '▲'; font-size: 10px; }

        /* Checkbox */
        .item-select {
            margin-left: 15px;
            transform: scale(1.5);
            accent-color: var(--primary-gold);
        }

        /* Selected Items Container */
        #selected-items-box {
            background-color: #fff9e6;
            border: 2px solid var(--primary-gold);
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 20px;
            display: none; /* Hidden initially */
        }
        #selected-items-box h3 {
            margin: 0 0 10px 0;
            font-size: 1.1rem;
            border-bottom: 1px solid var(--primary-gold);
            padding-bottom: 5px;
        }
        .selected-item-row {
            display: flex;
            justify-content: space-between;
            font-size: 0.95rem;
            margin-bottom: 5px;
        }

        /* --- GOOGLE REVIEW PAGE --- */
        .review-card {
            background: white;
            border-radius: 12px;
            padding: 25px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }
        .g-rating-score {
            font-size: 3rem;
            font-weight: 700;
            color: var(--primary-dark);
        }
        .g-stars {
            color: #f4b400;
            font-size: 1.5rem;
            margin: 5px 0;
        }
        .g-count {
            color: #777;
            font-size: 0.9rem;
            margin-bottom: 25px;
        }
        .g-btn {
            background-color: var(--google-blue);
            color: white;
            text-decoration: none;
            padding: 12px 25px;
            border-radius: 25px;
            font-weight: 600;
            display: inline-block;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
        }

        /* --- LOCATION PAGE --- */
        .map-preview {
            width: 100%;
            height: 250px;
            background-color: #e0e0e0;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #777;
            margin-bottom: 20px;
            background-image: url('https://maps.googleapis.com/maps/api/staticmap?center=Waluj,Maharashtra&zoom=14&size=400x250&key=YOUR_API_KEY'); /* Placeholder approach */
            background-size: cover;
            background-position: center;
            position: relative;
        }
        /* Using a CSS pattern to simulate a map for demo without API Key */
        .map-placeholder-visual {
            width: 100%; height: 100%;
            background: #e6e6e6;
            background-image: radial-gradient(#ccc 1px, transparent 1px);
            background-size: 20px 20px;
            border-radius: 12px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: bold;
        }

        .directions-btn {
            display: block;
            width: 100%;
            background-color: var(--primary-dark);
            color: white;
            text-align: center;
            padding: 15px;
            border-radius: 8px;
            text-decoration: none;
            font-size: 1.1rem;
            font-weight: 600;
        }

        /* --- FOOTER --- */
        footer {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            background-color: #222;
            color: #aaa;
            font-size: 0.75rem;
            padding: 10px 15px;
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
            z-index: 100;
        }
        .footer-left { text-align: left; }
        .footer-right { text-align: right; max-width: 50%; }

    </style>
</head>
<body>

<div id="app-container">
    
    <header>
        <div class="logo-area">
            <img src="https://cdn-icons-png.flaticon.com/512/10232/10232497.png" alt="Hotel Bhondawe Palace Logo"> 
        </div>
        <div class="hotel-name">Hotel Bhondawe Palace</div>
    </header>

    <div id="landing-page" class="page active">
        <div style="height: 20px;"></div>
        
        <div class="landing-btn" onclick="showPage('menu-page')">
            🍽️ Hotel Menu
        </div>
        
        <div class="landing-btn" onclick="showPage('review-page')">
            ⭐ Google Review
        </div>
        
        <div class="landing-btn" onclick="showPage('location-page')">
            📍 Location / Directions
        </div>
    </div>

    <div id="menu-page" class="page">
        <button class="back-btn" onclick="showPage('landing-page')">Back to Home</button>
        
        <div id="selected-items-box">
            <h3>Your Selected Items</h3>
            <div id="selected-list-content">
                </div>
            <div style="margin-top:10px; font-weight:bold; text-align:right; border-top:1px dashed #ccc; padding-top:5px;">
                Total Estimate: ₹<span id="total-price">0</span>
            </div>
        </div>

        <div id="menu-content">
            </div>
    </div>

    <div id="review-page" class="page">
        <button class="back-btn" onclick="showPage('landing-page')">Back to Home</button>
        
        <div class="review-card">
            <img src="https://upload.wikimedia.org/wikipedia/commons/5/53/Google_%22G%22_Logo.svg" alt="Google" width="40" style="margin-bottom:10px;">
            <h2>Hotel Bhondawe Palace</h2>
            <div class="g-rating-score">4.1</div>
            <div class="g-stars">★★★★☆</div>
            <div class="g-count">128 Google Reviews</div>
            
            <a href="https://search.google.com/local/writereview?placeid=YOUR_PLACE_ID" target="_blank" class="g-btn">
                Rate & Review on Google
            </a>
            <p style="margin-top:15px; font-size:0.8rem; color:#888;">Your feedback helps us serve you better!</p>
        </div>
    </div>

    <div id="location-page" class="page">
        <button class="back-btn" onclick="showPage('landing-page')">Back to Home</button>
        
        <div class="map-preview">
            <div class="map-placeholder-visual">
                Map Preview
            </div>
        </div>
        
        <div style="background:white; padding:20px; border-radius:12px; margin-bottom:20px;">
            <h3 style="margin-top:0;">Address:</h3>
            <p style="color:#555; line-height:1.6;">
                Plot no 4,5,6,7 & 8,<br>
                Gut no 379,<br>
                Waluj BK Nagar Highway,<br>
                Waluj, Gangapur,<br>
                Maharashtra 431133
            </p>
        </div>

        <a href="https://www.google.com/maps/dir/?api=1&destination=Waluj+BK+Nagar+Highway+Maharashtra" target="_blank" class="directions-btn">
            📍 Get Directions
        </a>
    </div>

    <footer>
        <div class="footer-left">
            📞 Contact:<br>
            <a href="tel:07887878774" style="color:#aaa; text-decoration:none;">0788 787 8774</a>
        </div>
        <div class="footer-right">
            📍 Waluj BK Nagar Highway,<br>
            Waluj, Gangapur
        </div>
    </footer>

</div>

<script>
    // --- MENU DATA ---
    const menuData = [
        {
            category: "Breakfast (नाश्ता)",
            items: [
                { name: "Misal Pav", desc: "Spicy sprouted curry with bread", price: 80, type: "veg" },
                { name: "Poha", desc: "Flattened rice with spices", price: 40, type: "veg" },
                { name: "Upma", desc: "Semolina porridge with veggies", price: 40, type: "veg" }
            ]
        },
        {
            category: "Starters",
            items: [
                { name: "Paneer Tikka", desc: "Grilled cottage cheese cubes", price: 220, type: "veg" },
                { name: "Hara Bhara Kabab", desc: "Spinach and green pea patties", price: 190, type: "veg" },
                { name: "Chicken Chilli", desc: "Spicy stir-fry chicken", price: 240, type: "nonveg" },
                { name: "Chicken 65", desc: "Deep fried spicy chicken", price: 230, type: "nonveg" }
            ]
        },
        {
            category: "Soups",
            items: [
                { name: "Tomato Soup", desc: "Rich and creamy", price: 110, type: "veg" },
                { name: "Manchow Soup", desc: "Spicy with fried noodles", price: 120, type: "veg" },
                { name: "Chicken Clear Soup", desc: "Healthy broth", price: 140, type: "nonveg" }
            ]
        },
        {
            category: "Main Course (Veg)",
            items: [
                { name: "Paneer Butter Masala", desc: "Rich tomato gravy", price: 240, type: "veg" },
                { name: "Veg Kolhapuri", desc: "Spicy mixed vegetable curry", price: 210, type: "veg" },
                { name: "Dal Tadka", desc: "Yellow lentils tempered with spices", price: 160, type: "veg" }
            ]
        },
        {
            category: "Main Course (Non-Veg)",
            items: [
                { name: "Butter Chicken", desc: "Creamy tomato chicken curry", price: 280, type: "nonveg" },
                { name: "Chicken Handi", desc: "Traditional clay pot curry", price: 260, type: "nonveg" },
                { name: "Mutton Masala", desc: "Spicy goat meat curry", price: 320, type: "nonveg" }
            ]
        },
        {
            category: "Breads",
            items: [
                { name: "Tandoori Roti", desc: "Whole wheat bread", price: 25, type: "veg" },
                { name: "Butter Roti", desc: "With glazed butter", price: 30, type: "veg" },
                { name: "Butter Naan", desc: "Refined flour bread", price: 45, type: "veg" },
                { name: "Garlic Naan", desc: "Infused with garlic", price: 55, type: "veg" }
            ]
        },
        {
            category: "Rice & Biryani",
            items: [
                { name: "Jeera Rice", desc: "Cumin flavored rice", price: 120, type: "veg" },
                { name: "Veg Biryani", desc: "Aromatic vegetable rice", price: 200, type: "veg" },
                { name: "Chicken Biryani", desc: "Layered chicken and rice", price: 250, type: "nonveg" }
            ]
        },
        {
            category: "Desserts & Beverages",
            items: [
                { name: "Gulab Jamun (2 pcs)", desc: "Sweet milk solids", price: 60, type: "veg" },
                { name: "Ice Cream", desc: "Vanilla / Chocolate / Strawberry", price: 50, type: "veg" },
                { name: "Mineral Water", desc: "1 Litre Bottle", price: 20, type: "veg" },
                { name: "Masala Chaas", desc: "Spiced buttermilk", price: 30, type: "veg" }
            ]
        }
    ];

    // --- RENDER MENU ---
    const menuContent = document.getElementById('menu-content');

    function renderMenu() {
        let html = '';
        menuData.forEach((section, sIndex) => {
            html += `<div class="menu-section-title">${section.category}</div>`;
            section.items.forEach((item, iIndex) => {
                const uniqueId = `item-${sIndex}-${iIndex}`;
                html += `
                <div class="menu-item">
                    <div class="item-details">
                        <div class="item-header">
                            <span class="icon-${item.type}"></span>
                            <span class="item-name">${item.name}</span>
                        </div>
                        <div class="item-desc">${item.desc}</div>
                        <div class="item-price">₹${item.price}</div>
                    </div>
                    <input type="checkbox" class="item-select" 
                        data-name="${item.name}" 
                        data-price="${item.price}" 
                        id="${uniqueId}"
                        onchange="updateSelection()">
                </div>`;
            });
        });
        menuContent.innerHTML = html;
    }

    // --- NAVIGATION LOGIC ---
    function showPage(pageId) {
        // Hide all pages
        document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
        // Show target page
        document.getElementById(pageId).classList.add('active');
        // Scroll to top
        window.scrollTo(0,0);
    }

    // --- SELECTION LOGIC ---
    function updateSelection() {
        const checkboxes = document.querySelectorAll('.item-select:checked');
        const box = document.getElementById('selected-items-box');
        const list = document.getElementById('selected-list-content');
        const totalSpan = document.getElementById('total-price');

        if (checkboxes.length === 0) {
            box.style.display = 'none';
            return;
        }

        box.style.display = 'block';
        list.innerHTML = '';
        let total = 0;

        checkboxes.forEach(chk => {
            const name = chk.getAttribute('data-name');
            const price = parseInt(chk.getAttribute('data-price'));
            total += price;

            list.innerHTML += `
                <div class="selected-item-row">
                    <span>${name}</span>
                    <span>₹${price}</span>
                </div>
            `;
        });

        totalSpan.innerText = total;
        // Scroll to selection box smoothly to show update
        // box.scrollIntoView({behavior: "smooth", block: "center"});
    }

    // Initialize
    renderMenu();

</script>

</body>
</html>
