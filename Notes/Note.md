1 ###Creating the list of the products
2 With \*ngFor, the <div> repeats for each product in the list.
3 The {{ product.name }} statement is an example of Angular's interpolation syntax. Interpolation {{ }} lets you render the property value as text.

<!-- creating the products
<h2>Products</h2>
<h2>Products</h2>
<div *ngFor="let product of products">
<h3>
details of product and link
  <a [title] = "product.name +  'details' ">
{{product.name}}
</a>
</h3>
product description
<p *ngIf="product.description">
Description: {{ product.description }}
</p>
button to share
<button type="button" (click)="share()">
Share
</button>

</div>
-->

4 To set up ProductAlertsComponent to receive product data, first import Input from @angular/core.

src/app/product-alerts/product-alerts.component.ts
content_copy

<!-- import { Component, OnInit, Input } from '@angular/core';
import { Product } from '../products'; -->

5 In the ProductAlertsComponent class definition, define a property named product with an @Input() decorator. The @Input() decorator indicates that the property value passes in from the component's parent, ProductListComponent.

src/app/product-alerts/product-alerts.component.ts
content_copy

<!-- export class ProductAlertsComponent implements OnInit {

  @Input() product!: Product;
  constructor() { }

  ngOnInit() {
  }

} -->

6 Open product-alerts.component.html and replace the placeholder paragraph with a Notify Me button that appears if the product price is over $700.

src/app/product-alerts/product-alerts.component.html
content_copy

<!-- <p *ngIf="product && product.price > 700">
  <button type="button">Notify Me</button>
</p> -->

7 The generator automatically added the ProductAlertsComponent to the AppModule to make it available to other components in the application.

src/app/app.module.ts
content_copy

<!-- import { ProductAlertsComponent } from './product-alerts/product-alerts.component';

@NgModule({
  declarations: [
    AppComponent,
    TopBarComponent,
    ProductListComponent,
    ProductAlertsComponent,
  ], -->

8 Finally, to display ProductAlertsComponent as a child of ProductListComponent, add the <app-product-alerts> element to product-list.component.html. Pass the current product as input to the component using property binding.

src/app/product-list/product-list.component.html
content_copy

<!-- <button type="button" (click)="share()">
  Share
</button>

<app-product-alerts
  [product]="product">
</app-product-alerts> -->

The new product alert component takes a product as input from the product list. With that input, it shows or hides the Notify Me button, based on the price of the product. The Phone XL price is over $700, so the Notify Me button appears on that product.
4 #To make each product name a link to product details, add the <a> element around {{ product.name }}.

5 Set the title to be the product's name by using the property binding [ ] syntax, as follows:

6 Add the product descriptions. On a <p> element, use an \*ngIf directive so that Angular only creates the <p> element if the current product has a description.
The application now displays the name and description of each product in the list. Notice that the final product does not have a description paragraph. Angular doesn't create the <p> element because the product's description property is empty.

