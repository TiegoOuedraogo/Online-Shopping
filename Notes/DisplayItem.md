Display the cart items
This section shows you how to use the cart service to display the products in the cart.

In cart.component.ts, import the CartService from the cart.service.ts file.

src/app/cart/cart.component.ts
content_copy
<!-- import { Component } from '@angular/core';
import { CartService } from '../cart.service';
Inject the CartService so that the CartComponent can use it by adding it to the constructor(). -->

src/app/cart/cart.component.ts
content_copy
<!-- export class CartComponent {


  constructor(
    private cartService: CartService
  ) { }
} -->
Define the items property to store the products in the cart.

src/app/cart/cart.component.ts
content_copy
<!-- export class CartComponent {

  items = this.cartService.getItems();

  constructor(
    private cartService: CartService
  ) { }
} -->
This code sets the items using the CartService getItems() method. You defined this method when you created cart.service.ts.

Update the cart template with a header, and use a <div> with an *ngFor to display each of the cart items with its name and price. The resulting CartComponent template is as follows.

src/app/cart/cart.component.html
content_copy
<!-- <h3>Cart</h3>

<div class="cart-item" *ngFor="let item of items">
  <span>{{ item.name }}</span>
  <span>{{ item.price | currency }}</span>
</div> -->
Verify that your cart works as expected:

Click My Store.
Click on a product name to display its details.
Click Buy to add the product to the cart.
Click Checkout to see the cart.