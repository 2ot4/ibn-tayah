<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مطعم وكافيه ابن تايه - Ibn Tayah Restaurant</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <style>
        :root {
            --primary: #d4af37;
            --primary-dark: #aa882c;
            --bg-dark: #121212;
            --card-bg: #1e1e1e;
            --text-light: #f5f5f5;
            --text-muted: #a0a0a0;
            --accent-red: #e63946;
            --success: #2ec4b6;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-light);
            padding-bottom: 80px;
        }

        header {
            background: linear-gradient(135deg, #1f1c18, #000000);
            padding: 20px 15px;
            text-align: center;
            border-bottom: 2px solid var(--primary);
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 4px 15px rgba(0,0,0,0.5);
        }

        .logo-area h1 {
            color: var(--primary);
            font-size: 1.8rem;
            margin-bottom: 5px;
            letter-spacing: 1px;
        }

        .logo-area p {
            color: var(--text-muted);
            font-size: 0.9rem;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 15px;
        }

        /* Search & Categories */
        .search-box {
            margin: 15px 0;
            position: relative;
        }

        .search-box input {
            width: 100%;
            padding: 12px 40px 12px 15px;
            border-radius: 25px;
            border: 1px solid #333;
            background-color: var(--card-bg);
            color: var(--text-light);
            font-size: 1rem;
            outline: none;
        }

        .search-box i {
            position: absolute;
            right: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--primary);
        }

        .categories {
            display: flex;
            gap: 10px;
            overflow-x: auto;
            padding: 10px 0;
            scrollbar-width: none;
        }

        .categories::-webkit-scrollbar {
            display: none;
        }

        .cat-btn {
            background-color: var(--card-bg);
            color: var(--text-light);
            padding: 8px 18px;
            border-radius: 20px;
            border: 1px solid #333;
            white-space: nowrap;
            cursor: pointer;
            transition: all 0.3s;
        }

        .cat-btn.active, .cat-btn:hover {
            background-color: var(--primary);
            color: #000;
            font-weight: bold;
            border-color: var(--primary);
        }

        /* Menu Grid */
        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .menu-card {
            background-color: var(--card-bg);
            border-radius: 12px;
            overflow: hidden;
            border: 1px solid #2a2a2a;
            display: flex;
            flex-direction: column;
            position: relative;
            transition: transform 0.2s;
        }

        .menu-card:hover {
            transform: translateY(-3px);
        }

        .menu-card img {
            width: 100%;
            height: 140px;
            object-fit: cover;
            background-color: #2a2a2a;
        }

        .card-body {
            padding: 12px;
            display: flex;
            flex-direction: column;
            flex-grow: 1;
        }

        .card-title {
            font-size: 1.1rem;
            margin-bottom: 5px;
            color: var(--text-light);
        }

        .card-price {
            color: var(--primary);
            font-weight: bold;
            font-size: 1rem;
            margin-bottom: 10px;
        }

        .card-actions {
            margin-top: auto;
            display: flex;
            gap: 5px;
        }

        .btn-add {
            flex: 1;
            background-color: var(--primary);
            color: #000;
            border: none;
            padding: 8px;
            border-radius: 6px;
            font-weight: bold;
            cursor: pointer;
        }

        .btn-edit {
            background-color: #333;
            color: var(--text-light);
            border: none;
            padding: 8px 12px;
            border-radius: 6px;
            cursor: pointer;
        }

        /* Cart Floating Bar */
        .cart-bar {
            position: fixed;
            bottom: 15px;
            left: 50%;
            transform: translateX(-50%);
            width: 90%;
            max-width: 770px;
            background-color: var(--primary);
            color: #000;
            padding: 12px 20px;
            border-radius: 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-weight: bold;
            box-shadow: 0 5px 20px rgba(212, 175, 55, 0.4);
            cursor: pointer;
            z-index: 99;
        }

        /* Modal / Cart Drawer */
        .modal {
            display: none;
            position: fixed;
            top: 0; left: 0; right: 0; bottom: 0;
            background-color: rgba(0,0,0,0.8);
            z-index: 1000;
            justify-content: center;
            align-items: flex-end;
        }

        .modal-content {
            background-color: var(--card-bg);
            width: 100%;
            max-width: 800px;
            max-height: 90vh;
            border-top-left-radius: 20px;
            border-top-right-radius: 20px;
            padding: 20px;
            overflow-y: auto;
            position: relative;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid #333;
            padding-bottom: 10px;
            margin-bottom: 15px;
        }

        .close-btn {
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--text-muted);
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid #2a2a2a;
        }

        .qty-controls {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .qty-btn {
            background-color: #333;
            color: white;
            border: none;
            width: 28px;
            height: 28px;
            border-radius: 50%;
            cursor: pointer;
        }

        .form-group {
            margin-bottom: 12px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-size: 0.9rem;
            color: var(--text-muted);
        }

        .form-group input, .form-group select {
            width: 100%;
            padding: 10px;
            border-radius: 8px;
            border: 1px solid #333;
            background-color: #121212;
            color: white;
        }

        .btn-submit {
            width: 100%;
            background-color: #25d366;
            color: white;
            border: none;
            padding: 12px;
            border-radius: 8px;
            font-weight: bold;
            font-size: 1rem;
            cursor: pointer;
            margin-top: 10px;
        }

        .admin-toggle {
            text-align: center;
            margin: 20px 0;
        }

        .btn-admin {
            background-color: transparent;
            color: var(--primary);
            border: 1px solid var(--primary);
            padding: 8px 16px;
            border-radius: 20px;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <header>
        <div class="logo-area">
            <h1><i class="fa-solid fa-utensils"></i> مطعم وكافيه ابن تايه</h1>
            <p>أطيب المأكولات والمشروبات البغدادية - بغداد</p>
        </div>
    </header>

    <div class="container">
        <div class="search-box">
            <i class="fa-solid fa-magnifying-glass"></i>
            <input type="text" id="searchInput" placeholder="ابحث عن وجبة أو مشروب..." onkeyup="filterItems()">
        </div>

        <div class="categories">
            <button class="cat-btn active" onclick="filterCategory('all', this)">الكل</button>
            <button class="cat-btn" onclick="filterCategory('وجبات رئيسية', this)">وجبات رئيسية</button>
            <button class="cat-btn" onclick="filterCategory('مشويات', this)">مشويات</button>
            <button class="cat-btn" onclick="filterCategory('وجبات سريعة', this)">وجبات سريعة</button>
            <button class="cat-btn" onclick="filterCategory('مقبلات', this)">مقبلات</button>
            <button class="cat-btn" onclick="filterCategory('مشروبات وحلويات', this)">مشروبات وحلويات</button>
        </div>

        <div class="menu-grid" id="menuGrid"></div>

        <div class="admin-toggle">
            <button class="btn-admin" onclick="openAdminModal()"><i class="fa-solid fa-gear"></i> لوحة الإدارة</button>
        </div>
    </div>

    <!-- Floating Cart Bar -->
    <div class="cart-bar" onclick="openCartModal()">
        <span><i class="fa-solid fa-cart-shopping"></i> السلة (<span id="cartCount">0</span>)</span>
        <span id="cartTotal">0 د.ع</span>
    </div>

    <!-- Cart Modal -->
    <div class="modal" id="cartModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>طلبك من مطعم ابن تايه</h2>
                <span class="close-btn" onclick="closeCartModal()">&times;</span>
            </div>
            <div id="cartItemsList"></div>

            <div style="margin: 15px 0; border-top: 1px solid #333; padding-top: 10px;">
                <div class="form-group">
                    <label>نوع الطلب:</label>
                    <select id="orderType" onchange="calculateDelivery()">
                        <option value="توصيل">توصيل (دليفري)</option>
                        <option value="سفري">سفري (استلام من المطعم)</option>
                        <option value="داخل المطعم">صالة (داخل المطعم)</option>
                    </select>
                </div>
                <div class="form-group" id="addressGroup">
                    <label>المنطقة في بغداد:</label>
                    <input type="text" id="customerAddress" placeholder="مثال: الكرادة، المنصور، الأعظمية...">
                </div>
                <div class="form-group">
                    <label>اسمك الكريـم:</label>
                    <input type="text" id="customerName" placeholder="أدخل اسمك">
                </div>
                <div class="form-group">
                    <label>رقم الهاتف:</label>
                    <input type="tel" id="customerPhone" placeholder="07XXXXXXXXX">
                </div>
                <div class="form-group">
                    <label>طريقة الدفع:</label>
                    <select id="paymentMethod">
                        <option value="كاش عند الاستلام">كاش عند الاستلام</option>
                        <option value="زين كاش ZainCash">زين كاش ZainCash</option>
                    </select>
                </div>
                <div style="display: flex; justify-content: space-between; font-weight: bold; margin: 10px 0; font-size: 1.1rem; color: var(--primary);">
                    <span>المجموع الكلي:</span>
                    <span id="finalModalTotal">0 د.ع</span>
                </div>
                <button class="btn-submit" onclick="sendWhatsAppOrder()"><i class="fa-brands fa-whatsapp"></i> إرسال الطلب عبر الواتساب</button>
            </div>
        </div>
    </div>

    <!-- Admin Modal -->
    <div class="modal" id="adminModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>إضافة وجبة جديدة</h2>
                <span class="close-btn" onclick="closeAdminModal()">&times;</span>
            </div>
            <div class="form-group">
                <label>اسم الوجبة:</label>
                <input type="text" id="newItemName">
            </div>
            <div class="form-group">
                <label>السعر (د.ع):</label>
                <input type="number" id="newItemPrice">
            </div>
            <div class="form-group">
                <label>التصنيف:</label>
                <select id="newItemCategory">
                    <option value="وجبات رئيسية">وجبات رئيسية</option>
                    <option value="مشويات">مشويات</option>
                    <option value="وجبات سريعة">وجبات سريعة</option>
                    <option value="مقبلات">مقبلات</option>
                    <option value="مشروبات وحلويات">مشروبات وحلويات</option>
                </select>
            </div>
            <div class="form-group">
                <label>رابط الصورة (أو اتركها افتراضية):</label>
                <input type="text" id="newItemImage" placeholder="https://...">
            </div>
            <button class="btn-submit" style="background-color: var(--primary); color: #000;" onclick="addNewItem()">إضافة الوجبة</button>
        </div>
    </div>

    <script>
        let menuItems = JSON.parse(localStorage.getItem('ibn_tayah_menu')) || [
            { id: 1, name: 'قوزي على تمن بغدادي', price: 15000, category: 'وجبات رئيسية', img: 'https://images.unsplash.com/photo-1544025162-d76694265947?w=500' },
            { id: 2, name: 'كيلو مشكل مشويات', price: 28000, category: 'مشويات', img: 'https://images.unsplash.com/photo-1555939594-58d7cb561ad1?w=500' },
            { id: 3, name: 'برغر ابن تايه الميجا', price: 8000, category: 'وجبات سريعة', img: 'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=500' },
            { id: 4, name: 'صحن مقبلات مشكل', price: 5000, category: 'مقبلات', img: 'https://images.unsplash.com/photo-1541529086526-db283c563270?w=500' },
            { id: 5, name: 'شاي بغدادي / استكان شاي', price: 1000, category: 'مشروبات وحلويات', img: 'https://images.unsplash.com/photo-1576092768241-dec231879fc3?w=500' }
        ];

        let cart = [];
        let currentCategory = 'all';

        function renderMenu() {
            const grid = document.getElementById('menuGrid');
            grid.innerHTML = '';
            
            const filtered = menuItems.filter(item => {
                const matchesCat = currentCategory === 'all' || item.category === currentCategory;
                const searchVal = document.getElementById('searchInput').value.toLowerCase();
                const matchesSearch = item.name.toLowerCase().includes(searchVal);
                return matchesCat && matchesSearch;
            });

            filtered.forEach(item => {
                grid.innerHTML += `
                    <div class="menu-card">
                        <img src="${item.img}" alt="${item.name}">
                        <div class="card-body">
                            <div class="card-title">${item.name}</div>
                            <div class="card-price">${item.price.toLocaleString()} د.ع</div>
                            <div class="card-actions">
                                <button class="btn-add" onclick="addToCart(${item.id})">إضافة للسلة</button>
                                <button class="btn-edit" onclick="deleteItem(${item.id})"><i class="fa-solid fa-trash"></i></button>
                            </div>
                        </div>
                    </div>
                `;
            });
        }

        function filterCategory(cat, btn) {
            currentCategory = cat;
            document.querySelectorAll('.cat-btn').forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            renderMenu();
        }

        function filterItems() {
            renderMenu();
        }

        function addToCart(id) {
            const item = menuItems.find(i => i.id === id);
            const cartItem = cart.find(c => c.id === id);
            if (cartItem) {
                cartItem.qty++;
            } else {
                cart.push({ ...item, qty: 1 });
            }
            updateCartUI();
        }

        function changeQty(id, delta) {
            const cartItem = cart.find(c => c.id === id);
            if (cartItem) {
                cartItem.qty += delta;
                if (cartItem.qty <= 0) {
                    cart = cart.filter(c => c.id !== id);
                }
            }
            updateCartUI();
            renderCartModal();
        }

        function updateCartUI() {
            const count = cart.reduce((sum, item) => sum + item.qty, 0);
            const total = cart.reduce((sum, item) => sum + (item.price * item.qty), 0);
            document.getElementById('cartCount').innerText = count;
            document.getElementById('cartTotal').innerText = total.toLocaleString() + ' د.ع';
        }

        function openCartModal() {
            renderCartModal();
            document.getElementById('cartModal').style.display = 'flex';
        }

        function closeCartModal() {
            document.getElementById('cartModal').style.display = 'none';
        }

        function renderCartModal() {
            const list = document.getElementById('cartItemsList');
            list.innerHTML = '';
            let subtotal = 0;

            if (cart.length === 0) {
                list.innerHTML = '<p style="text-align:center; color: var(--text-muted);">السلة فارغة حالياً</p>';
            } else {
                cart.forEach(item => {
                    subtotal += item.price * item.qty;
                    list.innerHTML += `
                        <div class="cart-item">
                            <div>
                                <div style="font-weight:bold;">${item.name}</div>
                                <div style="color:var(--primary); font-size:0.85rem;">${(item.price * item.qty).toLocaleString()} د.ع</div>
                            </div>
                            <div class="qty-controls">
                                <button class="qty-btn" onclick="changeQty(${item.id}, -1)">-</button>
                                <span>${item.qty}</span>
                                <button class="qty-btn" onclick="changeQty(${item.id}, 1)">+</button>
                            </div>
                        </div>
                    `;
                });
            }
            calculateDelivery();
        }

        function calculateDelivery() {
            const type = document.getElementById('orderType').value;
            const subtotal = cart.reduce((sum, item) => sum + (item.price * item.qty), 0);
            let deliveryFee = (type === 'توصيل') ? 3000 : 0;
            
            document.getElementById('addressGroup').style.display = (type === 'توصيل') ? 'block' : 'none';
            document.getElementById('finalModalTotal').innerText = (subtotal + deliveryFee).toLocaleString() + ' د.ع';
        }

        function sendWhatsAppOrder() {
            if (cart.length === 0) {
                alert('يرجى إضافة وجبات للسلة أولاً!');
                return;
            }

            const name = document.getElementById('customerName').value || 'زبون كريم';
            const phone = document.getElementById('customerPhone').value || 'غير محدد';
            const type = document.getElementById('orderType').value;
            const address = document.getElementById('customerAddress').value || 'بغداد';
            const payment = document.getElementById('paymentMethod').value;

            let msg = `*طلب جديد - مطعم وكافيه ابن تايه* 🍔🍕%0A%0A`;
            msg += `*الاسم:* ${name}%0A`;
            msg += `*الهاتف:* ${phone}%0A`;
            msg += `*نوع الطلب:* ${type}%0A`;
            if (type === 'توصيل') msg += `*العنوان:* ${address}%0A`;
            msg += `*طريقة الدفع:* ${payment}%0A%0A`;
            msg += `*التفاصيل:*%0A`;

            let subtotal = 0;
            cart.forEach(item => {
                subtotal += item.price * item.qty;
                msg += `- ${item.name} (x${item.qty}) = ${(item.price * item.qty).toLocaleString()} د.ع%0A`;
            });

            let deliveryFee = (type === 'توصيل') ? 3000 : 0;
            if (deliveryFee > 0) msg += `*خدمة التوصيل:* 3,000 د.ع%0A`;
            msg += `%0A*المجموع الكلي:* ${(subtotal + deliveryFee).toLocaleString()} د.ع`;

            const restaurantPhone = "9647700000000"; // رقم واتساب المطعم
            window.open(`https://wa.me/${restaurantPhone}?text=${msg}`, '_blank');
        }

        function openAdminModal() { document.getElementById('adminModal').style.display = 'flex'; }
        function closeAdminModal() { document.getElementById('adminModal').style.display = 'none'; }

        function addNewItem() {
            const name = document.getElementById('newItemName').value;
            const price = parseInt(document.getElementById('newItemPrice').value);
            const category = document.getElementById('newItemCategory').value;
            const img = document.getElementById('newItemImage').value || 'https://images.unsplash.com/photo-1546069901-ba9599a7e63c?w=500';

            if (!name || !price) {
                alert('يرجى كتابة الاسم والسعر!');
                return;
            }

            const newItem = { id: Date.now(), name, price, category, img };
            menuItems.push(newItem);
            localStorage.setItem('ibn_tayah_menu', JSON.stringify(menuItems));
            renderMenu();
            closeAdminModal();
        }

        function deleteItem(id) {
            if (confirm('هل أنت تأكد من حذف هذه الوجبة؟')) {
                menuItems = menuItems.filter(i => i.id !== id);
                localStorage.setItem('ibn_tayah_menu', JSON.stringify(menuItems));
                renderMenu();
            }
        }

        // Initialize
        renderMenu();
    </script>
</body>
</html>
