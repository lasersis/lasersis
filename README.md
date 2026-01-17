<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Склад для діодного станка</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
            color: #fff;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1000px;
            margin: 0 auto;
        }

        header {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 30px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            text-align: center;
        }

        h1 {
            font-size: 2.5em;
            color: #00d9ff;
            text-shadow: 0 0 20px rgba(0, 217, 255, 0.5);
        }

        .add-button {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, #00d9ff 0%, #0099cc 100%);
            border: none;
            border-radius: 50%;
            font-size: 2em;
            color: #000;
            cursor: pointer;
            box-shadow: 0 5px 20px rgba(0, 217, 255, 0.4);
            transition: all 0.3s;
            z-index: 1000;
        }

        .add-button:hover {
            transform: scale(1.1) rotate(90deg);
            box-shadow: 0 8px 30px rgba(0, 217, 255, 0.6);
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            z-index: 2000;
            align-items: center;
            justify-content: center;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
            padding: 30px;
            border-radius: 15px;
            max-width: 600px;
            width: 90%;
            max-height: 90vh;
            overflow-y: auto;
            border: 2px solid rgba(0, 217, 255, 0.3);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .modal-header h2 {
            color: #00d9ff;
        }

        .close-btn {
            background: none;
            border: none;
            color: #fff;
            font-size: 2em;
            cursor: pointer;
            transition: all 0.3s;
        }

        .close-btn:hover {
            color: #ff0055;
            transform: rotate(90deg);
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #00d9ff;
            font-weight: 500;
        }

        input, textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid rgba(0, 217, 255, 0.3);
            border-radius: 8px;
            background: rgba(255, 255, 255, 0.05);
            color: #fff;
            font-size: 1em;
            transition: all 0.3s;
        }

        input:focus, textarea:focus {
            outline: none;
            border-color: #00d9ff;
            box-shadow: 0 0 15px rgba(0, 217, 255, 0.3);
        }

        textarea {
            resize: vertical;
            min-height: 80px;
        }

        .btn {
            padding: 12px 30px;
            border: none;
            border-radius: 8px;
            font-size: 1.1em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .btn-primary {
            background: linear-gradient(135deg, #00d9ff 0%, #0099cc 100%);
            color: #000;
            width: 100%;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(0, 217, 255, 0.4);
        }

        .items-list {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            overflow: hidden;
        }

        .item {
            display: flex;
            gap: 20px;
            padding: 20px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            transition: all 0.3s;
            align-items: center;
        }

        .item:hover {
            background: rgba(0, 217, 255, 0.1);
            border-left: 4px solid #00d9ff;
        }

        .item:last-child {
            border-bottom: none;
        }

        .item-image {
            width: 150px;
            height: 150px;
            border: 3px solid #cc0044;
            border-radius: 8px;
            object-fit: cover;
            background: rgba(255, 255, 255, 0.05);
            flex-shrink: 0;
        }

        .item-content {
            flex: 1;
        }

        .item-title {
            font-size: 1.5em;
            color: #fff;
            font-weight: bold;
            margin-bottom: 10px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .item-title:hover {
            color: #00d9ff;
        }

        .item-description {
            color: #a0a0a0;
            line-height: 1.6;
            margin-bottom: 10px;
        }

        .item-meta {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin-top: 10px;
        }

        .meta-badge {
            background: rgba(0, 217, 255, 0.15);
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 0.85em;
            border: 1px solid rgba(0, 217, 255, 0.3);
        }

        .item-actions {
            display: flex;
            gap: 10px;
            flex-direction: column;
        }

        .btn-link {
            background: linear-gradient(135deg, #0066ff 0%, #0044cc 100%);
            color: #fff;
            padding: 10px 20px;
            border-radius: 8px;
            text-decoration: none;
            display: inline-block;
            transition: all 0.3s;
            text-align: center;
            font-weight: bold;
        }

        .btn-link:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 102, 255, 0.4);
        }

        .btn-delete {
            background: linear-gradient(135deg, #ff0055 0%, #cc0044 100%);
            color: #fff;
            padding: 10px 20px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: bold;
        }

        .btn-delete:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(255, 0, 85, 0.4);
        }

        .empty-state {
            text-align: center;
            padding: 60px 20px;
            color: #666;
        }

        .empty-state h3 {
            margin-top: 20px;
            font-size: 1.5em;
        }

        @media (max-width: 768px) {
            .item {
                flex-direction: column;
            }

            .item-image {
                width: 100%;
                height: 200px;
            }

            .item-actions {
                flex-direction: row;
                width: 100%;
            }

            .btn-link, .btn-delete {
                flex: 1;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🔧 Склад для діодного станка</h1>
        </header>

        <div id="itemsContainer">
            <div class="empty-state">
                <h3>📦 Склад порожній</h3>
                <p>Натисніть синю кнопку внизу, щоб додати товар</p>
            </div>
        </div>
    </div>

    <button class="add-button" onclick="openModal()">+</button>

    <div id="modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>➕ Додати товар</h2>
                <button class="close-btn" onclick="closeModal()">×</button>
            </div>
            
            <div class="form-group">
                <label for="itemName">Назва товару *</label>
                <input type="text" id="itemName" placeholder="Наприклад: Діоди 1N4007" required>
            </div>

            <div class="form-group">
                <label for="itemImage">URL картинки *</label>
                <input type="url" id="itemImage" placeholder="https://example.com/image.jpg" required>
            </div>

            <div class="form-group">
                <label for="itemDescription">Опис товару</label>
                <textarea id="itemDescription" placeholder="Введіть опис товару..."></textarea>
            </div>

            <div class="form-group">
                <label for="itemLink">Посилання на товар</label>
                <input type="url" id="itemLink" placeholder="https://example.com/product">
            </div>

            <button class="btn btn-primary" onclick="addItem()">Додати товар</button>
        </div>
    </div>

    <script>
        let items = [];

        async function loadItems() {
            try {
                const result = await window.storage.list('product:', true);
                if (result && result.keys && result.keys.length > 0) {
                    const promises = result.keys.map(async (key) => {
                        try {
                            const data = await window.storage.get(key, true);
                            return data ? JSON.parse(data.value) : null;
                        } catch (e) {
                            return null;
                        }
                    });
                    const loadedItems = await Promise.all(promises);
                    items = loadedItems.filter(item => item !== null);
                } else {
                    items = [];
                }
            } catch (error) {
                console.log('Перше завантаження');
                items = [];
            }
            renderItems();
        }

        function openModal() {
            document.getElementById('modal').classList.add('active');
        }

        function closeModal() {
            document.getElementById('modal').classList.remove('active');
            document.getElementById('itemName').value = '';
            document.getElementById('itemImage').value = '';
            document.getElementById('itemDescription').value = '';
            document.getElementById('itemLink').value = '';
        }

        async function addItem() {
            const name = document.getElementById('itemName').value.trim();
            const image = document.getElementById('itemImage').value.trim();
            const description = document.getElementById('itemDescription').value.trim();
            const link = document.getElementById('itemLink').value.trim();

            if (!name || !image) {
                alert('Будь ласка, заповніть назву та URL картинки!');
                return;
            }

            const item = {
                id: Date.now().toString(),
                name,
                image,
                description,
                link,
                addedAt: new Date().toLocaleString('uk-UA')
            };

            try {
                await window.storage.set(`product:${item.id}`, JSON.stringify(item), true);
                items.push(item);
                closeModal();
                renderItems();
            } catch (error) {
                alert('Помилка при додаванні товару');
            }
        }

        async function deleteItem(id) {
            if (!confirm('Видалити цей товар?')) {
                return;
            }

            try {
                await window.storage.delete(`product:${id}`, true);
                items = items.filter(item => item.id !== id);
                renderItems();
            } catch (error) {
                alert('Помилка при видаленні');
            }
        }

        function openLink(url) {
            if (url) {
                window.open(url, '_blank');
            }
        }

        function renderItems() {
            const container = document.getElementById('itemsContainer');
            
            if (items.length === 0) {
                container.innerHTML = `
                    <div class="empty-state">
                        <h3>📦 Склад порожній</h3>
                        <p>Натисніть синю кнопку внизу, щоб додати товар</p>
                    </div>
                `;
                return;
            }

            const itemsHTML = items.map(item => `
                <div class="item">
                    <img src="${item.image}" alt="${item.name}" class="item-image" onerror="this.src='data:image/svg+xml,%3Csvg xmlns=%22http://www.w3.org/2000/svg%22 width=%22150%22 height=%22150%22%3E%3Crect width=%22150%22 height=%22150%22 fill=%22%23333%22/%3E%3Ctext x=%2250%25%22 y=%2250%25%22 text-anchor=%22middle%22 dy=%22.3em%22 fill=%22%23666%22 font-size=%2220%22%3EНемає фото%3C/text%3E%3C/svg%3E'">
                    <div class="item-content">
                        <div class="item-title" onclick="openLink('${item.link}')">${item.name}</div>
                        ${item.description ? `<div class="item-description">${item.description}</div>` : ''}
                        <div class="item-meta">
                            <span class="meta-badge">🕐 ${item.addedAt}</span>
                        </div>
                    </div>
                    <div class="item-actions">
                        ${item.link ? `<a href="${item.link}" target="_blank" class="btn-link">🔗 Перейти</a>` : ''}
                        <button class="btn-delete" onclick="deleteItem('${item.id}')">🗑️ Видалити</button>
                    </div>
                </div>
            `).join('');

            container.innerHTML = `<div class="items-list">${itemsHTML}</div>`;
        }

        loadItems();
    </script>
</body>
</html>
