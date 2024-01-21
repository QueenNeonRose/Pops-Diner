<html>
<head>
  <title>Menu Calculator</title>
    <style>
    body {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 250vh;
      text-align: center;
    }
	.total-box {
		display: flex;
		justify-content: center; /* Center horizontally */
		align-items: center; /* Center vertically */
		margin-top: 20px;
	}}
	
	 .calculate-button {
      width: 150px; /* Adjust the desired width */
      height: 50px; /* Adjust the desired height */
    }
	
	.submit-button {
      width: 150px; /* Adjust the desired width */
      height: 40px; /* Adjust the desired height */
    }
	
	.reset-button {
      width: 150px; /* Adjust the desired width */
      height: 30px; /* Adjust the desired height */
    }
    
    h1 {
      margin-bottom: 20px;
    }
    
    h2 {
      margin-top: 20px;
    }
	
	h3 {
      border: 1px solid black; /* Adjust the border style as needed */
      padding: 5px; /* Add padding to create space around the heading */
    }
    
    .menu-items {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      gap: 10px;
      margin-bottom: 10px;
    }
    
    .menu-items div {
      display: flex;
      align-items: center;
    }
    
    .total-box {
      display: flex;
      justify-content: flex-end;
      align-self: Center;
      margin-top: 20px;
    }
    
    .button-container {
      display: flex;
      gap: 10px;
      margin-top: 20px;
    }
	
	.menu-items div img {
      width: 50px; /* Adjust the desired width */
      height: 50px; /* Adjust the desired height */
      margin-left: 10px; /* Add margin as per your preference */
    }
    {
    button {
      margin-top: 20px;
	}}}}}}
  </style>
  <script>
    function calculateTotal() {
    var total = 0;
    var checkboxes = document.querySelectorAll('input[type="checkbox"]:checked');

    checkboxes.forEach(function(checkbox) {
      var quantityInput = checkbox.parentNode.querySelector('input[type="number"]');
      var quantity = parseInt(quantityInput.value);
      var price = parseFloat(checkbox.value);

      if (checkbox.value === '-25%') {
        var itemPrice = total * 0.25;
        total -= itemPrice;
      } else if (checkbox.value === '-30%') {
        var itemPrice = total * 0.3;
        total -= itemPrice;
      } else if (checkbox.value === '-50%') {
        var itemPrice = total * 0.5;
        total -= itemPrice;
      } else {
        total += price * quantity;
      }
    });

    var totalElement = document.getElementById('total');
    totalElement.textContent = total.toFixed(2);

    var discountTotalElement = document.getElementById('discount-total');
    var discount = total * 0.5;
    discountTotalElement.textContent = discount.toFixed(2);
  }


    
    function submitOrder() {
    var name = document.getElementById('name').value;
    if (name.trim() === '') {
      alert('Please enter a name.');
      return;
    }

    // Collect selected items and their quantities
    var selectedItems = [];
    var checkboxes = document.querySelectorAll('input[type="checkbox"]:checked');
    checkboxes.forEach(function (checkbox) {
      var itemName = checkbox.nextElementSibling.textContent;
      var quantityInput = checkbox.parentNode.querySelector('input[type="number"]');
      var quantity = parseInt(quantityInput.value);
      var price = parseFloat(checkbox.value);
      selectedItems.push({ name: itemName, quantity: quantity, price: price });
    });

    var total = 0;
    var discountTotal = 0;

    selectedItems.forEach(function (item) {
      if (item.price < 0) {
        var discountPercentage = Math.abs(item.price);
        var itemDiscount = total * (discountPercentage / 100);
        discountTotal += itemDiscount;
      } else {
        total += item.price * item.quantity;
      }
    });

    var commission = (total * 0.5).toFixed(2);
    var totalWithDiscount = total - discountTotal;

    alert('Order submitted!');

    var discordWebhookURL = 'https://discord.com/api/webhooks/1198701843073728652/M0zZTw-BNiNGRb9fWPialCDCRifLsLrcOHalGsQBtDcU9Cz8eHrUhC1nAvzERd6S6hGH';

    var xhr = new XMLHttpRequest();
    xhr.open('POST', discordWebhookURL, true);
    xhr.setRequestHeader('Content-Type', 'application/json');

    var message = {
      content: 'New order!',
      embeds: [{
        title: 'Order Details',
        fields: [
          {
            name: 'Name',
            value: name,
            inline: true
          },
          {
            name: 'Total',
            value: '$' + total ,
            inline: true
          },
          {
            name: 'Discount Total',
            value: '$' + discountTotal.toFixed(2),
            inline: true
          },
          {
            name: 'Commission (50%)',
            value: '$' + commission,
            inline: true
          },
          {
            name: 'Ordered Items',
            value: selectedItems.map(item => `${item.name} x${item.quantity} - $${(item.price * item.quantity).toFixed(2)}`).join('\n'),
            inline: false
          }
        ]
      }]
    };

    xhr.send(JSON.stringify(message));
  }

function resetCalculator() {
  var checkboxes = document.querySelectorAll('input[type="checkbox"]');
  var quantityInputs = document.querySelectorAll('input[type="number"]');
  
  checkboxes.forEach(function(checkbox) {
    checkbox.checked = false;
  });
  
  quantityInputs.forEach(function(quantityInput) {
    quantityInput.value = 1;
  });
  
  document.getElementById('total').textContent = '0.00';
}
	function submitAndReset() {
	submitOrder();
	resetCalculator();
}

  </script>
</head>
<body>
	
<div style="margin-bottom: 25px;"></div>
 
<body style="background-color:#276dd6;">
  <h1>Menu Calculator</h1>
  
  <h2>Menu Items</h2>

  <div style="margin-bottom: 10px;"></div>
  
  <h3>Breakfast</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="450$">
    <label for="Velmachoice">Bacon and Eggs - $</label>450
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="450$">
    <label for="Davechoice">Bacon and Toast - $</label>450
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="450$">
    <label for="Davechoice">Sausage and Eggs - $</label>450
    <input type="number" value="1" min="1">
  </div>
  
   <h3>Lunch</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="450$">
    <label for="Velmachoice">Cheese Burger - $</label>450
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="450$">
    <label for="Davechoice">Hamburger - $</label>450
    <input type="number" value="1" min="1">
  </div>
  
   <div>
    <input type="checkbox" id="Davechoice" value="450$">
    <label for="Davechoice">Steak Burger - $</label>450
    <input type="number" value="1" min="1">
  </div>
   
   <div>
    <input type="checkbox" id="Davechoice" value="350$">
    <label for="Davechoice">BLT Sandwich - $</label>350
    <input type="number" value="1" min="1">
  </div>
    
   <div>
    <input type="checkbox" id="Davechoice" value="350$">
    <label for="Davechoice">Cheese Sandwich - $</label>350
    <input type="number" value="1" min="1">
  </div>
    
   <div>
    <input type="checkbox" id="Davechoice" value="350$">
    <label for="Davechoice">Egg Sandwich - $</label>350
    <input type="number" value="1" min="1">
  </div>
    
   <div>
    <input type="checkbox" id="Davechoice" value="350$">
    <label for="Davechoice">Ham n Cheese Sandwich - $</label>350
    <input type="number" value="1" min="1">
  </div>
    
   <div>
    <input type="checkbox" id="Davechoice" value="350$">
    <label for="Davechoice">Ham Sandwich - $</label>350
    <input type="number" value="1" min="1">
  </div>
    
   <div>
    <input type="checkbox" id="Davechoice" value="350$">
    <label for="Davechoice">Tuna Sandwich - $</label>350
    <input type="number" value="1" min="1">
  </div>
    
   <div>
    <input type="checkbox" id="Davechoice" value="350$">
    <label for="Davechoice">Grilled Wrap - $</label>350
    <input type="number" value="1" min="1">
  </div>
    
   <div>
    <input type="checkbox" id="Davechoice" value="350$">
    <label for="Davechoice">Ranch Wrap - $</label>350
    <input type="number" value="1" min="1">
  </div>
    
   <div>
    <input type="checkbox" id="Davechoice" value="350$">
    <label for="Davechoice">Veggie Wrap - $</label>350
    <input type="number" value="1" min="1">
  </div>
 
   <h3>Dessert</h3>

  <div style="margin-bottom: 10px;"></div>
  
 <div>
    <input type="checkbox" id="Davechoice" value="250$">
    <label for="Davechoice">Carrot Cake - $</label>250
    <input type="number" value="1" min="1">
  </div>

 <div>
    <input type="checkbox" id="Davechoice" value="250$">
    <label for="Davechoice">Cheese Cake - $</label>250
    <input type="number" value="1" min="1">
  </div>
  
 <div>
    <input type="checkbox" id="Davechoice" value="250$">
    <label for="Davechoice">Jello - $</label>250
    <input type="number" value="1" min="1">
  </div>
  
 <div>
    <input type="checkbox" id="Davechoice" value="250$">
    <label for="Davechoice">Chocolate Pudding - $</label>250
    <input type="number" value="1" min="1">
  </div>
  
 <div>
    <input type="checkbox" id="Davechoice" value="250$">
    <label for="Davechoice">Donuts - $</label>250
    <input type="number" value="1" min="1">
  </div>
  
 <div>
    <input type="checkbox" id="Davechoice" value="250$">
    <label for="Davechoice">Icecream cones - $</label>250
    <input type="number" value="1" min="1">
  </div>

  
   <h3> Drinks</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="150$">
    <label for="Velmachoice">Ecola- $</label>150
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="uwueats" value="150$">
    <label for="Velmachoice">Ecola Light- $</label>150
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="uwueats" value="150$">
    <label for="Velmachoice">Sprunk- $</label>150
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="uwueats" value="150$">
    <label for="Velmachoice">Sprunk Light- $</label>150
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="uwueats" value="150$">
    <label for="Velmachoice">Coffee- $</label>150
    <input type="number" value="1" min="1">
  </div>


   
  <h3>Specials</h3>
   <div>
    <input type="checkbox" id="Davechoice" value="1350$">
    <label for="Davechoice">Powdered French Toast - $</label>1350
    <input type="number" value="1" min="1">
  </div>

<div style="margin-bottom: 10px;"></div>
  
  <h3> Discount Items</h3> 

<div>
  <input type="checkbox" id="50off" value="-50%">
  <label for="50off">Employee Discount - 50% off</label>
  <input type="number" value="1" min="1" max="1">
</div>

<div>
  <input type="checkbox" id="30off" value="-30%">
  <label for="25off">Mechs/PD & EMS - 30% off</label>
  <input type="number" value="1" min="1" max="1">
</div>

<h3> Delivery </h3>
  
  <div>
    <input type="checkbox" id="ColinChoice" value="1000"><!--The price is the value, change that and then the name and itll change on the menu-->
    <label for="ColinChoice">Delivery Fee - $</label>1000
    <input type="number" value="1" min="1">
  </div>
  

  
  <div style="margin-bottom: 25px;"></div>


<div>
    <label for="name">Cashier's Name:</label>
    <input type="text" id="name">
  </div>
  

<div style="margin-bottom: 25px;"></div>
 
<div class="total-box">
  <span>Total: $</span>
  <span id="total">0.00</span>
</div>
  
  
  <div style="margin-bottom: 45px;"></div>
  

  <button class="calculate-button" onclick="calculateTotal()">Calculate Total</button>
  <button class="submit-button" onclick="submitAndReset()">Submit Order</button>
  <button class="reset-button" onclick="resetCalculator()">Reset</button>

 
  
  
  <div style="margin-bottom: 10px;"></div>
