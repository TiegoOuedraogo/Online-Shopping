Using forms for user input
This guide builds on the Managing Data step of the Getting Started tutorial, Get started with a basic Angular app.

This section walks you through adding a form-based checkout feature to collect user information as part of checkout.

Define the checkout form model
This step shows you how to set up the checkout form model in the component class. The form model determines the status of the form.

Open cart.component.ts.

Import the FormBuilder service from the @angular/forms package. This service provides convenient methods for generating controls.

src/app/cart/cart.component.ts
content_copy

<!-- import { Component } from '@angular/core';
import { FormBuilder } from '@angular/forms';

import { CartService } from '../cart.service'; -->

Inject the FormBuilder service in the CartComponent constructor(). This service is part of the ReactiveFormsModule module, which you've already imported.

src/app/cart/cart.component.ts
content_copy

<!-- export class CartComponent {

  constructor(
    private cartService: CartService,
    private formBuilder: FormBuilder,
  ) {}
} -->

To gather the user's name and address, use the FormBuilder group() method to set the checkoutForm property to a form model containing name and address fields.

src/app/cart/cart.component.ts
content_copy

<!-- export class CartComponent {

  items = this.cartService.getItems();

  checkoutForm = this.formBuilder.group({
    name: '',
    address: ''
  });

  constructor(
    private cartService: CartService,
    private formBuilder: FormBuilder,
  ) {}
} -->

Define an onSubmit() method to process the form. This method allows users to submit their name and address. In addition, this method uses the clearCart() method of the CartService to reset the form and clear the cart.

The entire cart component class is as follows:

src/app/cart/cart.component.ts
content_copy

<!-- import { Component } from '@angular/core';
import { FormBuilder } from '@angular/forms';

import { CartService } from '../cart.service';

@Component({
  selector: 'app-cart',
  templateUrl: './cart.component.html',
  styleUrls: ['./cart.component.css']
})
export class CartComponent {

  items = this.cartService.getItems();

  checkoutForm = this.formBuilder.group({
    name: '',
    address: ''
  });

  constructor(
    private cartService: CartService,
    private formBuilder: FormBuilder,
  ) {}

  onSubmit(): void {
    // Process checkout data here
    this.items = this.cartService.clearCart();
    console.warn('Your order has been submitted', this.checkoutForm.value);
    this.checkoutForm.reset();
  }
}-->

Create the checkout form
Use the following steps to add a checkout form at the bottom of the Cart view.

At the bottom of cart.component.html, add an HTML <form> element and a Purchase button.

Use a formGroup property binding to bind checkoutForm to the HTML <form>.

src/app/cart/cart.component.html
content_copy

<!-- <form [formGroup]="checkoutForm">

  <button class="button" type="submit">Purchase</button>

</form> -->

On the form tag, use an ngSubmit event binding to listen for the form submission and call the onSubmit() method with the checkoutForm value.

src/app/cart/cart.component.html (cart component template detail)
content_copy

<!-- <form [formGroup]="checkoutForm" (ngSubmit)="onSubmit()">
</form> -->

Add <input> fields for name and address, each with a formControlName attribute that binds to the checkoutForm form controls for name and address to their <input> fields. The complete component is as follows:

src/app/cart/cart.component.html
content_copy

<!-- <h3>Cart</h3>

<p>
  <a routerLink="/shipping">Shipping Prices</a>
</p>

<div class="cart-item" *ngFor="let item of items">
  <span>{{ item.name }} </span>
  <span>{{ item.price | currency }}</span>
</div>

<form [formGroup]="checkoutForm" (ngSubmit)="onSubmit()">

  <div>
    <label for="name">
      Name
    </label>
    <input id="name" type="text" formControlName="name">
  </div>

  <div>
    <label for="address">
      Address
    </label>
    <input id="address" type="text" formControlName="address">
  </div>

  <button class="button" type="submit">Purchase</button>

</form>-->

After putting a few items in the cart, users can review their items, enter their name and address, and submit their purchase.
