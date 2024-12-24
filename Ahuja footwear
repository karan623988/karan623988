<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ahuja Footwear - Admin & Shop</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f4f4f4;
      color: #333;
    }
    header {
      background: linear-gradient(45deg, #FF6F61, #FF3D4E);
      color: white;
      text-align: center;
      padding: 50px 0;
    }
    .container {
      max-width: 800px;
      margin: auto;
      padding: 20px;
    }
    .product-form {
      display: none;
      background: #fff;
      padding: 20px;
      border: 1px solid #ddd;
      border-radius: 10px;
      margin-bottom: 20px;
    }
    .product {
      background: white;
      border: 1px solid #ddd;
      padding: 15px;
      margin: 10px 0;
      border-radius: 10px;
      text-align: center;
    }
    .product img {
      max-width: 100%;
      height: auto;
      border-radius: 5px;
    }
    .btn {
      padding: 10px 15px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1rem;
      margin-top: 10px;
    }
    .btn-buy {
      background-color: #28a745;
      color: white;
    }
    .btn-buy:hover {
      background-color: #218838;
    }
    .btn-delete {
      background-color: #dc3545;
      color: white;
    }
    .btn-delete:hover {
      background-color: #c82333;
    }
  </style>
</head>
<body>

<header>
  <h1>Ahuja Footwear</h1>
  <p>Admin Panel & Product List</p>
</header>

<div class="container">
  <h2>Admin Login</h2>
  <button onclick="checkPassword()">Login as Admin</button>

  <div class="product-form" id="productForm">
    <h3>Add Product</h3>
    <input type="text" id="productName" placeholder="Product Name"><br>
    <input type="number" id="productPrice" placeholder="Product Price"><br>
    <input type="text" id="productSize" placeholder="Product Sizes (e.g., S, M, L)"><br>
    <input type="file" id="productImage" accept="image/*"><br>
    <button class="btn" onclick="addProduct()">Add Product</button>
  </div>

  <h2>Product List</h2>
  <div id="productList"></div>
</div>

<script>
  const correctPassword = "karan1234";
  let isAdminLoggedIn = false;
  let products = JSON.parse(localStorage.getItem('products')) || [];

  // Function to check password for admin login
  function checkPassword() {
    const enteredPassword = prompt("Enter Admin Password:");
    if (enteredPassword === correctPassword) {
      isAdminLoggedIn = true;
      alert("Admin Access Granted");
      document.getElementById("productForm").style.display = "block"; // Show Add Product Form
      renderProductList();
    } else {
      alert("Incorrect Password");
    }
  }

  // Function to add a product
  function addProduct() {
    const name = document.getElementById("productName").value;
    const price = document.getElementById("productPrice").value;
    const size = document.getElementById("productSize").value;
    const imageFile = document.getElementById("productImage").files[0];

    if (!name || !price || !size || !imageFile) {
      alert("All fields are required!");
      return;
    }

    const reader = new FileReader();
    reader.onloadend = function () {
      const product = {
        id: Date.now(),
        name,
        price,
        size,
        image: reader.result,
      };

      products.push(product);
      localStorage.setItem('products', JSON.stringify(products));
      renderProductList();
    };
    reader.readAsDataURL(imageFile);
  }

  // Function to render the product list
  function renderProductList() {
    const productList = document.getElementById("productList");
    productList.innerHTML = "";

    if (products.length === 0) {
      productList.innerHTML = "<p>No products available. Add some products.</p>";
      return;
    }

    products.forEach((product) => {
      const productCard = `
        <div class="product">
          <img src="${product.image}" alt="${product.name}">
          <h3>${product.name}</h3>
          <p>Price: ₹${product.price}</p>
          <p>Sizes: ${product.size}</p>
          ${
            isAdminLoggedIn
              ? `<button class="btn btn-delete" onclick="deleteProduct(${product.id})">Delete</button>`
              : `<button class="btn btn-buy" onclick="buyProduct('${product.name}')">Buy Now</button>`
          }
        </div>
      `;
      productList.innerHTML += productCard;
    });
  }

  // Function to delete a product
  function deleteProduct(productId) {
    products = products.filter(product => product.id !== productId);
    localStorage.setItem('products', JSON.stringify(products));
    renderProductList();
  }

  // Function to handle "Buy Now" button click
  function buyProduct(productName) {
    const message = `Hi, I want to buy the product: ${productName}`;
    const whatsappURL = `https://wa.me/6239883897?text=${encodeURIComponent(message)}`;
    window.open(whatsappURL, "_blank");
  }

  // Load products on page load
  window.onload = renderProductList;
</script>

</body>
</html>
