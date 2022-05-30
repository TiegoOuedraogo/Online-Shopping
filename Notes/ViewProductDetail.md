            View product details

The ProductDetailsComponent handles the display of each product. The Angular Router displays components based on the browser's URL and your defined routes.

In this section, you'll use the Angular Router to combine the products data and route information to display the specific details for each product.

1 In product-details.component.ts, import ActivatedRoute from @angular/router, and the products array from ../products.

src/app/product-details/product-details.component.ts
content_copy

<!-- import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

import { Product, products } from '../products'; -->

2 Define the product property.

src/app/product-details/product-details.component.ts
content_copy

<!-- export class ProductDetailsComponent implements OnInit {

  product: Product | undefined;
  /* ... */
} -->

3 Inject ActivatedRoute into the constructor() by adding private route: ActivatedRoute as an argument within the constructor's parentheses.

src/app/product-details/product-details.component.ts
content_copy

<!-- export class ProductDetailsComponent implements OnInit {

  product: Product | undefined;

  constructor(private route: ActivatedRoute) { }

} -->

ActivatedRoute is specific to each component that the Angular Router loads. ActivatedRoute contains information about the route and the route's parameters.

By injecting ActivatedRoute, you are configuring the component to use a service. The Managing Data step covers services in more detail.

4 In the ngOnInit() method, extract the productId from the route parameters and find the corresponding product in the products array.

src/app/product-details/product-details.component.ts
content_copy

<!-- ngOnInit() {
  // First get the product id from the current route.
  const routeParams = this.route.snapshot.paramMap;
  const productIdFromRoute = Number(routeParams.get('productId'));

  // Find the product that correspond with the id provided in route.
  this.product = products.find(product => product.id === productIdFromRoute);
} -->

The route parameters correspond to the path variables you define in the route. To access the route parameters, we use route.snapshot, which is the ActivatedRouteSnapshot that contains information about the active route at that particular moment in time. The URL that matches the route provides the productId . Angular uses the productId to display the details for each unique product.

5 Update the ProductDetailsComponent template to display product details with an \*ngIf. If a product exists, the <div> renders with a name, price, and description.

src/app/product-details/product-details.component.html
content_copy

<!-- <h2>Product Details</h2>

<div *ngIf="product">
  <h3>{{ product.name }}</h3>
  <h4>{{ product.price | currency }}</h4>
  <p>{{ product.description }}</p>
</div> -->

The line, <h4>{{ product.price | currency }}</h4>, uses the currency pipe to transform product.price from a number to a currency string. A pipe is a way you can transform data in your HTML template. For more information about Angular pipes, see Pipes.

When users click on a name in the product list, the router navigates them to the distinct URL for the product, shows the ProductDetailsComponent, and displays the product details.
