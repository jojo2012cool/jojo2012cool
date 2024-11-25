
document.addEventListener('DOMContentLoaded', () => {
    const cart = [];
    const cartItemsContainer = document.querySelector('.cart-items');
    const totalPriceEl = document.getElementById('total-price');

    function updateCart() {
        cartItemsContainer.innerHTML = '';
        let total = 0;

        cart.forEach((item) => {
            const div = document.createElement('div');
            div.textContent = `${item.name} - ${item.price}€ x ${item.quantity}`;
            cartItemsContainer.appendChild(div);
            total += item.price * item.quantity;
        });

        totalPriceEl.textContent = total.toFixed(2);
    }

    document.querySelectorAll('.add-to-cart').forEach((button) => {
        button.addEventListener('click', () => {
            const productEl = button.parentElement;
            const id = productEl.getAttribute('data-id');
            const name = productEl.getAttribute('data-name');
            const price = parseFloat(productEl.getAttribute('data-price'));

            const existingItem = cart.find((item) => item.id === id);
            if (existingItem) {
                existingItem.quantity++;
            } else {
                cart.push({ id, name, price, quantity: 1 });
            }

            updateCart();
        });
    });

    document.getElementById('checkout').addEventListener('click', () => {
        if (cart.length === 0) {
            alert('Ihr Warenkorb ist leer!');
        } else {
            alert('Vielen Dank für Ihren Einkauf!');
            cart.length = 0;
            updateCart();
        }
    });
});
