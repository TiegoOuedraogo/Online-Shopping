Create the cart view
For customers to see their cart, you can create the cart view in two steps:

Create a cart component and configure routing to the new component.
Display the cart items.
Set up the cart component
To create the cart view, follow the same steps you did to create the ProductDetailsComponent and configure routing for the new component.

Generate a new component named cart in the terminal by running the following command:
ng generate component cart
content_copy
ng generate component cart
This command will generate the cart.component.ts file and its associated template and styles files.

src/app/cart/cart.component.ts
content_copy

<!-- import { Component } from '@angular/core';

@Component({
  selector: 'app-cart',
  templateUrl: './cart.component.html',
  styleUrls: ['./cart.component.css']
})
export class CartComponent {

  constructor() { }

} -->

StackBlitz also generates an ngOnInit() by default in components. You can ignore the CartComponent ngOnInit() for this tutorial.

Notice that the newly created CartComponent is added to the module's declarations in app.module.ts.

src/app/app.module.ts
content_copy

<!-- import { CartComponent } from './cart/cart.component';

@NgModule({
  declarations: [
    AppComponent,
    TopBarComponent,
    ProductListComponent,
    ProductAlertsComponent,
    ProductDetailsComponent,
    CartComponent,
  ], -->

Still in app.module.ts, add a route for the component CartComponent, with a path of cart.

src/app/app.module.ts
content_copy

<!-- @NgModule({
  imports: [
    BrowserModule,
    ReactiveFormsModule,
    RouterModule.forRoot([
      { path: '', component: ProductListComponent },
      { path: 'products/:productId', component: ProductDetailsComponent },
      { path: 'cart', component: CartComponent },
    ])
  ], -->

Update the Checkout button so that it routes to the /cart URL. In top-bar.component.html, add a routerLink directive pointing to /cart.

src/app/top-bar/top-bar.component.html
content_copy

<!-- <a routerLink="/cart" class="button fancy-button">
  <i class="material-icons">shopping_cart</i>Checkout
</a> -->

Verify the new CartComponent works as expected by clicking the Checkout button. You can see the "cart works!" default text, and the URL has the pattern https://getting-started.stackblitz.io/cart, where getting-started.stackblitz.io may be different for your StackBlitz project.
