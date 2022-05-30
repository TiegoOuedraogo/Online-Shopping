                Pass data to a parent component

To make the Notify Me button work, the child component needs to notify and pass the data to the parent component. The ProductAlertsComponent needs to emit an event when the user clicks Notify Me and the ProductListComponent needs to respond to the event.

In new components, the Angular Generator includes an empty constructor(), the OnInit interface, and the ngOnInit() method. Since these steps don't use them, the following code examples omit them for brevity.

1 In product-alerts.component.ts, import Output and EventEmitter from @angular/core.

src/app/product-alerts/product-alerts.component.ts
content_copy

<!-- import { Component, Input, Output, EventEmitter } from '@angular/core';
import { Product } from '../products'; -->

2 In the component class, define a property named notify with an @Output() decorator and an instance of EventEmitter(). Configuring ProductAlertsComponent with an @Output() allows the ProductAlertsComponent to emit an event when the value of the notify property changes.

src/app/product-alerts/product-alerts.component.ts
content_copy

<!-- export class ProductAlertsComponent {
  @Input() product: Product | undefined;
  @Output() notify = new EventEmitter();
} -->

3 In product-alerts.component.html, update the Notify Me button with an event binding to call the notify.emit() method.

src/app/product-alerts/product-alerts.component.html
content_copy

<!-- <p *ngIf="product && product.price > 700">
  <button type="button" (click)="notify.emit()">Notify Me</button>
</p> -->

4 Define the behavior that happens when the user clicks the button. The parent, ProductListComponent —not the ProductAlertsComponent— acts when the child raises the event. In product-list.component.ts, define an onNotify() method, similar to the share() method.

src/app/product-list/product-list.component.ts
content_copy

<!-- export class ProductListComponent {

  products = products;

  share() {
    window.alert('The product has been shared!');
  }

  onNotify() {
    window.alert('You will be notified when the product goes on sale');
  }
} -->

5 Update the ProductListComponent to receive data from the ProductAlertsComponent.

In product-list.component.html, bind <app-product-alerts> to the onNotify() method of the product list component. <app-product-alerts> is what displays the Notify Me button.

src/app/product-list/product-list.component.html
content_copy

<!-- <button type="button" (click)="share()">
  Share
</button>

<app-product-alerts
  [product]="product"
  (notify)="onNotify()">
</app-product-alerts> -->

6.  Click the Notify Me button to trigger an alert which reads, "You will be notified when the product goes on sale".
