<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Zuciosly</title>

<style>
body{font-family:Arial;margin:0;background:#f4f4f4}
header{background:black;color:white;padding:15px;display:flex;justify-content:space-between}
h1{margin:0}
input{padding:8px}
.banner{background:#222;color:white;text-align:center;padding:60px}
.filters{display:flex;gap:10px;padding:10px;overflow:auto}
.filters button{padding:8px;background:black;color:white;border:none}
.products{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;padding:10px}
.product{background:white;padding:10px;border-radius:5px;text-align:center}
.cart{position:fixed;bottom:10px;right:10px;background:black;color:white;padding:10px;border-radius:5px}
button{cursor:pointer}
footer{background:black;color:white;text-align:center;padding:10px;margin-top:20px}
</style>
</head>

<body>

<header>
<h1>Zuciosly</h1>
<input placeholder="Search..." onkeyup="search(this.value)">
</header>

<div class="banner">
<h2>Modern Style for Everyone</h2>
<p>Men | Women | Shoes | Sunglasses</p>
</div>

<div class="filters">
<button onclick="filter('all')">All</button>
<button onclick="filter('men')">Men</button>
<button onclick="filter('women')">Women</button>
<button onclick="filter('shoes')">Shoes</button>
<button onclick="filter('sunglasses')">Sunglasses</button>
</div>

<div class="products" id="products"></div>

<div class="cart">
Cart: <span id="count">0</span><br>
<button onclick="checkout()">Checkout</button>
</div>

<footer>
<p>Pay via M-Pesa / Tigo Pesa / Airtel Money</p>
<p>WhatsApp: 07XXXXXXXX</p>
</footer>

<script>

let products = [
{name:"Classic Shirt",price:35000,cat:"men",img:"LINK_YA_PICHA"},
{name:"Black Jeans",price:45000,cat:"men",img:"LINK_YA_PICHA"},
{name:"Polo T-shirt",price:25000,cat:"men",img:"LINK_YA_PICHA"},
{name:"Elegant Dress",price:50000,cat:"women",img:"LINK_YA_PICHA"},
{name:"Ladies Top",price:28000,cat:"women",img:"LINK_YA_PICHA"},
{name:"Maxi Dress",price:55000,cat:"women",img:"LINK_YA_PICHA"},
{name:"Sneakers",price:60000,cat:"shoes",img:"LINK_YA_PICHA"},
{name:"Heels",price:55000,cat:"shoes",img:"LINK_YA_PICHA"},
{name:"Sandals",price:30000,cat:"shoes",img:"LINK_YA_PICHA"},
{name:"Black Sunglasses",price:20000,cat:"sunglasses",img:"LINK_YA_PICHA"},
{name:"Gold Sunglasses",price:25000,cat:"sunglasses",img:"LINK_YA_PICHA"},
];

let cart = [];

function display(list){
 let html="";
 list.forEach(p=>{
  html+=`
  <div class="product">
  <img src="https://via.placeholder.com/150">
  <h3>${p.name}</h3>
  <p>${p.price} TZS</p>
  <button onclick="add('${p.name}',${p.price})">Add</button>
  </div>`;
 });
 document.getElementById("products").innerHTML=html;
}

display(products);

function filter(cat){
 if(cat==="all"){display(products);return;}
 display(products.filter(p=>p.cat===cat));
}

function search(text){
 text=text.toLowerCase();
 display(products.filter(p=>p.name.toLowerCase().includes(text)));
}

function add(name,price){
 cart.push({name,price});
 document.getElementById("count").innerText=cart.length;
}

function checkout(){
 if(cart.length===0){alert("Cart empty");return;}

 let msg="ORDER ZUCIOSLY:%0A";
 let total=0;

 cart.forEach(i=>{
  msg+="- "+i.name+" ("+i.price+" TZS)%0A";
  total+=i.price;
 });

 msg+="Total: "+total+" TZS%0A";
 msg+="Payment: M-Pesa / Tigo Pesa / Airtel Money";

 let phone="255617228206";

 window.open("https://wa.me/"+phone+"?text="+msg);
}

</script>

</body>
</html>
