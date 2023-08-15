
# My HTML

```html
<hr>
<h5 class="text-center">Ads</h5>

{% if ads_product %}
 <div class="container">
  <div class="row justify-content-center">

    <!-- Add more products here if needed -->
    <div class="col-md-2" style="border: 1px solid #ddd; padding: 15px; text-align: center; margin: 5px;">
      <img src="product_image.jpg" alt="Product 1" style="max-width: 100%; height: auto;">
      <h4>Product 1</h4>
      <button class="btn btn-primary">Buy Now</button>
    </div>
    <div class="col-md-2" style="border: 1px solid #ddd; padding: 15px; text-align: center; margin: 5px;">
      <img src="product_image.jpg" alt="Product 2" style="max-width: 100%; height: auto;">
      <h4>Product 2</h4>
      <button class="btn btn-primary">Buy Now</button>
    </div>
    <div class="col-md-2" style="border: 1px solid #ddd; padding: 15px; text-align: center; margin: 5px;">
      <img src="product_image.jpg" alt="Product 3" style="max-width: 100%; height: auto;">
      <h4>Product 3</h4>
      <button class="btn btn-primary">Buy Now</button>
    </div>
    <!-- Add more products here if needed -->

  </div>
</div>
{% else %}
<p class="text-center p-3">..... Ads Not Awailable .....</p>
{% endif %}
<hr>
```