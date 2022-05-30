                  Associate a URL path with a component

    The application already uses the Angular Router to navigate to the ProductListComponent. This section shows you how to define a route to show individual product details.

1 Generate a new component for product details. In the terminal generate a new product-details component by running the following command:

content_copy
ng generate component product-details
2 In app.module.ts, add a route for product details, with a path of products/:productId and ProductDetailsComponent for the component.

src/app/app.module.ts
content_copy

<!--  -->

3 Open product-list.component.html.

4 Modify the product name anchor to include a routerLink with the product.id as a parameter.

src/app/product-list/product-list.component.html
content_copy

<!-- <div *ngFor="let product of products">

  <h3>
    <a
      [title]="product.name + ' details'"
      [routerLink]="['/products', product.id]">
      {{ product.name }}
    </a>
  </h3>

  <!-- . . . -->

</div> -->
The RouterLink directive helps you customize the anchor element. In this case, the route, or URL, contains one fixed segment, /products. The final segment is variable, inserting the id property of the current product. For example, the URL for a product with an id of 1 would be similar to https://getting-started-myfork.stackblitz.io/products/1.

5 Verify that the router works as intended by clicking the product name. The application should display the ProductDetailsComponent, which currently says "product-details works!"

Notice that the URL in the preview window changes. The final segment is products/# where # is the number of the route you clicked.
