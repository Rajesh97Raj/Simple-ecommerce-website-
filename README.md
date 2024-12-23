let cart = [];
let cartBtn = document.getElementById('cart-btn');
let cartModal = document.getElementById('cart-modal');
let closeBtn = document.getElementById('close-btn');
let checkoutBtn = document.getElementById('checkout-btn');
let cartItems = document.getElementById('cart-items');
let totalElem = document.getElementById('total');

// Function to update the cart display
function updateCart() {
  let cartCount = cart.length;
  let total = cart.reduce((sum, item) => sum + item.price, 0).toFixed(2);
  cartBtn.innerText = `Cart (${cartCount})`;
  totalElem.innerText = `Total: $${total}`;

  // Display cart items in the modal
  cartItems.innerHTML = '';
  cart.forEach(item => {
    let itemElem = document.createElement('div');
    itemElem.innerText = `${item.name} - $${item.price}`;
    cartItems.appendChild(itemElem);
  });
}

// Event listener for adding products to the cart
let addToCartBtns = document.querySelectorAll('.add-to-cart');
addToCartBtns.forEach(btn => {
  btn.addEventListener('click', function() {
    const product = {
      id: this.dataset.id,
      name: this.dataset.name,
      price: parseFloat(this.dataset.price)
    };
    cart.push(product);
    updateCart();
  });
});

// Open cart modal
cartBtn.addEventListener('click', function() {
  cartModal.style.display = 'flex';
});

// Close cart modal
closeBtn.addEventListener('click', function() {
  cartModal.style.display = 'none';
});

// Checkout button (for now just logs the cart to console)
checkoutBtn.addEventListener('click', function() {
  alert('Checkout complete!');
  cart = [];
  updateCart();
  cartModal.style.display = 'none';
});
