<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>dashboard - tortitos</title>
  <link href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
</head>

<body>
  <!-- Header Section -->
  <header class="bg-dark text-white py-3 text-center">
    <h1 class="m-0 text-lowercase">orderlist</h1>
  </header>

  <!-- Dashboard Content -->
  <div class="container mt-4">
    <h2 class="text-center mb-4 text-lowercase">your order history</h2>
    <div id="orderSummary" class="text-left mb-3 text-lowercase"></div>
    <div class="text-center mt-4">
      <button class="btn btn-danger text-lowercase" onclick="clearHistory()">clear order history</button>
    </div>
  </div>

  <script>
    function displayOrders() {
      const orders = JSON.parse(localStorage.getItem('orderHistory')) || [];
      const orderContainer = document.getElementById('orderSummary');
      if (orders.length) {
        orderContainer.innerHTML = orders.map(order => `
          <div class="border p-3 mb-2">
            <p><strong>name:</strong> ${order.name}</p>
            <p><strong>contact:</strong> ${order.contact}</p>
            <p><strong>items:</strong></p>
            <ul>
              ${order.items.map(item => <li>${item.product} - ${item.quantity}</li>).join('')}
            </ul>
          </div>
        `).join('');
      } else {
        orderContainer.innerHTML = "<p>no orders placed yet.</p>";
      }
    }

    function clearHistory() {
      localStorage.removeItem('orderHistory');
      alert("Order history cleared.");
      displayOrders();
    }

    window.onload = function () {
      displayOrders();
    };
  </script>
</body>
</html>
