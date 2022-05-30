Retrieve shipping prices
Servers often return data in the form of a stream. Streams are useful because they make it easy to transform the returned data and make modifications to the way you request that data. Angular HttpClient is a built-in way to fetch data from external APIs and provide them to your application as a stream.

This section shows you how to use HttpClient to retrieve shipping prices from an external file.

The application that StackBlitz generates for this guide comes with predefined shipping data in assets/shipping.json. Use this data to add shipping prices for items in the cart.

src/assets/shipping.json
content_copy

<!-- [
  {
    "type": "Overnight",
    "price": 25.99
  },
  {
    "type": "2-Day",
    "price": 9.99
  },
  {
    "type": "Postal",
    "price": 2.99
  }
] -->

Configure AppModule to use HttpClient
To use Angular's HttpClient, you must configure your application to use HttpClientModule.

Angular's HttpClientModule registers the providers your application needs to use the HttpClient service throughout your application.

In app.module.ts, import HttpClientModule from the @angular/common/http package at the top of the file with the other imports. As there are a number of other imports, this code snippet omits them for brevity. Be sure to leave the existing imports in place.

src/app/app.module.ts
content_copy
import { HttpClientModule } from '@angular/common/http';
To register Angular's HttpClient providers globally, add HttpClientModule to the AppModule @NgModule() imports array.

src/app/app.module.ts
content_copy
@NgModule({

  <!-- imports: [
    BrowserModule,
    HttpClientModule,
    ReactiveFormsModule,
    RouterModule.forRoot([
      { path: '', component: ProductListComponent },
      { path: 'products/:productId', component: ProductDetailsComponent },
      { path: 'cart', component: CartComponent },
    ])
  ], -->
  <!-- declarations: [
    AppComponent,
    TopBarComponent,
    ProductListComponent,
    ProductAlertsComponent,
    ProductDetailsComponent,
    CartComponent,
  ],
  bootstrap: [
    AppComponent
  ]
}) -->

export class AppModule { }
Configure CartService to use HttpClient
The next step is to inject the HttpClient service into your service so your application can fetch data and interact with external APIs and resources.

In cart.service.ts, import HttpClient from the @angular/common/http package.

src/app/cart.service.ts
content_copy

<!-- import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Product } from './products';
Inject HttpClient into the CartService constructor(). -->

src/app/cart.service.ts
content_copy
export class CartService {

  <!-- items: Product[] = [];

  constructor(
    private http: HttpClient
  ) {}
/* . . . */
} -->

Configure CartService to get shipping prices
To get shipping data, from shipping.json, You can use the HttpClient get() method.

In cart.service.ts, below the clearCart() method, define a new getShippingPrices() method that uses the HttpClient get() method.

src/app/cart.service.ts
content_copy

<!-- export class CartService {
/* . . . */
  getShippingPrices() {
    return this.http.get<{type: string, price: number}[]>('/assets/shipping.json');
  }
} -->

For more information about Angular's HttpClient, see the Client-Server Interaction guide.
