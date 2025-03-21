<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tienda Online</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }

        header {
            background-color: #333;
            color: white;
            padding: 15px 0;
            text-align: center;
        }

        nav {
            background-color: #444;
            padding: 10px;
            text-align: center;
        }

        nav a {
            color: white;
            margin: 10px;
            text-decoration: none;
            font-weight: bold;
        }

        .container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            margin: 20px;
        }

        .product {
            background-color: white;
            border-radius: 8px;
            margin: 10px;
            padding: 15px;
            width: 200px;
            text-align: center;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        .product img {
            width: 100%;
            border-radius: 5px;
        }

        .product h3 {
            margin: 15px 0;
        }

        .product p {
            color: #555;
        }

        .product button {
            background-color: #28a745;
            color: white;
            border: none;
            padding: 10px;
            width: 100%;
            cursor: pointer;
            border-radius: 5px;
        }

        .product button:hover {
            background-color: #218838;
        }

        footer {
            background-color: #333;
            color: white;
            text-align: center;
            padding: 10px 0;
            position: fixed;
            width: 100%;
            bottom: 0;
        }

        .modal {
            display: none;
            position: fixed;
            z-index: 1;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0,0,0,0.4);
        }

        .modal-content {
            background-color: white;
            margin: 15% auto;
            padding: 20px;
            border-radius: 10px;
            width: 40%;
        }

        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
        }

        .close:hover,
        .close:focus {
            color: black;
            text-decoration: none;
            cursor: pointer;
        }
    </style>
</head>
<body>

<header>
    <h1>Tienda Online</h1>
    <p>Compra tus productos favoritos desde casa</p>
</header>

<nav>
    <a href="#">Inicio</a>
    <a href="#" onclick="verCarrito()">Carrito (<span id="carrito-count">0</span>)</a>
    <a href="#">Contacto</a>
</nav>

<div class="container">
    <div class="product">
        <img src="https://via.placeholder.com/200" alt="Producto 1">
        <h3>Producto 1</h3>
        <p>Descripción del producto 1.</p>
        <p><strong>$25.99</strong></p>
        <button onclick="agregarAlCarrito('Producto 1', 25.99)">Agregar al carrito</button>
    </div>
    <div class="product">
        <img src="https://via.placeholder.com/200" alt="Producto 2">
        <h3>Producto 2</h3>
        <p>Descripción del producto 2.</p>
        <p><strong>$35.99</strong></p>
        <button onclick="agregarAlCarrito('Producto 2', 35.99)">Agregar al carrito</button>
    </div>
    <div class="product">
        <img src="https://via.placeholder.com/200" alt="Producto 3">
        <h3>Producto 3</h3>
        <p>Descripción del producto 3.</p>
        <p><strong>$45.99</strong></p>
        <button onclick="agregarAlCarrito('Producto 3', 45.99)">Agregar al carrito</button>
    </div>
</div>

<footer>
    <p>&copy; 2025 Tienda Online. Todos los derechos reservados.</p>
</footer>

<!-- Modal para el carrito -->
<div id="modal-carrito" class="modal">
    <div class="modal-content">
        <span class="close" onclick="cerrarModal()">&times;</span>
        <h2>Carrito de Compras</h2>
        <div id="carrito-items"></div>
        <p><strong>Total: $<span id="carrito-total">0.00</span></strong></p>
        <button onclick="realizarCompra()">Realizar Compra</button>
    </div>
</div>

<script>
    let carrito = JSON.parse(localStorage.getItem('carrito')) || [];

    function actualizarCarrito() {
        // Actualiza el contador de artículos en el carrito
        const carritoCount = document.getElementById('carrito-count');
        carritoCount.innerText = carrito.length;

        // Actualiza el contenido del modal
        const carritoItems = document.getElementById('carrito-items');
        const carritoTotal = document.getElementById('carrito-total');

        carritoItems.innerHTML = '';
        let total = 0;

        carrito.forEach(item => {
            carritoItems.innerHTML += `<p>${item.nombre} - $${item.precio}</p>`;
            total += item.precio;
        });

        carritoTotal.innerText = total.toFixed(2);

        // Guarda el carrito en el almacenamiento local
        localStorage.setItem('carrito', JSON.stringify(carrito));
    }

    function agregarAlCarrito(nombre, precio) {
        carrito.push({ nombre, precio });
        actualizarCarrito();
    }

    function verCarrito() {
        const modal = document.getElementById('modal-carrito');
        modal.style.display = "block";
        actualizarCarrito();
    }

    function cerrarModal() {
        const modal = document.getElementById('modal-carrito');
        modal.style.display = "none";
    }

    function realizarCompra() {
        if (carrito.length === 0) {
            alert("Tu carrito está vacío.");
            return;
        }

        alert("Compra realizada exitosamente.");
        carrito = [];
        actualizarCarrito();
        cerrarModal();
    }

    // Cierra el modal si se hace clic fuera de él
    window.onclick = function(event) {
        const modal = document.getElementById('modal-carrito');
        if (event.target === modal) {
            cerrarModal();
        }
    };

    // Inicializa el carrito cuando se carga la página
    document.addEventListener("DOMContentLoaded", actualizarCarrito);
</script>

</body>