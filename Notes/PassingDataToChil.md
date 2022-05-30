Pass data to a child component

1 Currently, the product list displays the name and description of each product. The ProductListComponent also defines a products property that contains imported data for each product from the products array in products.ts.

The next step is to create a new alert feature that uses product data from the ProductListComponent. The alert checks the product's price, and, if the price is greater than $700, displays a Notify Me button that lets users sign up for notifications when the product goes on sale.

This section walks you through creating a child component, ProductAlertsComponent that can receive data from its parent component, ProductListComponent.

Click on the plus sign above the current terminal to create a new terminal to run the command to generate the component.

2 In the new terminal, generate a new component named product-alerts by running the following command.

content_copy
ng generate component product-alerts
The generator creates starter files for the three parts of the component:

product-alerts.component.ts
product-alerts.component.html
product-alerts.component.css

3 Open product-alerts.component.ts. The @Component() decorator indicates that the following class is a component. @Component() also provides metadata about the component, including its selector, templates, and styles.

<!-- import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-product-alerts',
  templateUrl: './product-alerts.component.html',
  styleUrls: ['./product-alerts.component.css']
})
export class ProductAlertsComponent implements OnInit {

  constructor() { }

  ngOnInit() {
  }

} -->

Key features in the @Component() are as follows:

The selector, app-product-alerts, identifies the component. By convention, Angular component selectors begin with the prefix app-, followed by the component name.

The template and style filenames reference the component's HTML and CSS

The @Component() definition also exports the class, ProductAlertsComponent, which handles functionality for the component
