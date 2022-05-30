Create a shipping component
Now that you've configured your application to retrieve shipping data, you can create a place to render that data.

Generate a cart component named shipping in the terminal by running the following command:

content_copy
ng generate component shipping
This command will generate the shipping.component.ts file and it associated template and styles files.

src/app/shipping/shipping.component.ts
content_copy

<!-- import { Component } from '@angular/core';

@Component({
  selector: 'app-shipping',
  templateUrl: './shipping.component.html',
  styleUrls: ['./shipping.component.css']
})
export class ShippingComponent {

  constructor() { }

}-->

In app.module.ts, add a route for shipping. Specify a path of shipping and a component of ShippingComponent.

src/app/app.module.ts
content_copy

<!-- @NgModule({
  imports: [
    BrowserModule,
    HttpClientModule,
    ReactiveFormsModule,
    RouterModule.forRoot([
      { path: '', component: ProductListComponent },
      { path: 'products/:productId', component: ProductDetailsComponent },
      { path: 'cart', component: CartComponent },
      { path: 'shipping', component: ShippingComponent },
    ])
  ],
  declarations: [
    AppComponent,
    TopBarComponent,
    ProductListComponent,
    ProductAlertsComponent,
    ProductDetailsComponent,
    CartComponent,
    ShippingComponent
  ],
  bootstrap: [
    AppComponent
  ]
})
export class AppModule { } -->

There's no link to the new shipping component yet, but you can see its template in the preview pane by entering the URL its route specifies. The URL has the pattern: https://angular-ynqttp--4200.local.webcontainer.io/shipping where the angular-ynqttp--4200.local.webcontainer.io part may be different for your StackBlitz project.

Configuring the ShippingComponent to use CartService
This section guides you through modifying the ShippingComponent to retrieve shipping data via HTTP from the shipping.json file.

In shipping.component.ts, import CartService.

src/app/shipping/shipping.component.ts
content_copy

<!-- import { Component } from '@angular/core';

import { CartService } from '../cart.service';
Inject the cart service in the ShippingComponent constructor(). -->

src/app/shipping/shipping.component.ts
content_copy
constructor(private cartService: CartService) { }
Define a shippingCosts property that sets the shippingCosts property using the getShippingPrices() method from the CartService.

src/app/shipping/shipping.component.ts
content_copy

<!-- export class ShippingComponent {

  shippingCosts = this.cartService.getShippingPrices();
}
Update the ShippingComponent template to display the shipping types and prices using the async pipe.

src/app/shipping/shipping.component.html
content_copy
<h3>Shipping Prices</h3>

<div class="shipping-item" *ngFor="let shipping of shippingCosts | async">
  <span>{{ shipping.type }}</span>
  <span>{{ shipping.price | currency }}</span>
</div> -->

The async pipe returns the latest value from a stream of data and continues to do so for the life of a given component. When Angular destroys that component, the async pipe automatically stops. For detailed information about the async pipe, see the AsyncPipe API documentation.

Add a link from the CartComponent view to the ShippingComponent view.

src/app/cart/cart.component.html
content_copy

<!-- <h3>Cart</h3>

<p>
  <a routerLink="/shipping">Shipping Prices</a>
</p>

<div class="cart-item" *ngFor="let item of items">
  <span>{{ item.name }}</span>
  <span>{{ item.price | currency }}</span>
</div> -->

Click the Checkout button to see the updated cart. Remember that changing the application causes the preview to refresh, which empties the cart.
