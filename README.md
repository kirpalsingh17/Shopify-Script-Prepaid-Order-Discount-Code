# Shopify-Script-Prepaid-Order-Discount-Code
Shopify Scripts for Prepaid Order by Discount Code

Shopify provides many features to extend functionality of core Shopify store. One of them is giving permission to create Shopify scripts. With these Shopify scripts, we can manipulate Shopify cart and checkout page.

Here, We are going to create script for discount code which apply to give discount and remove COD payment method.

<h3>Offer discount code if opt for the prepaid option</h3>
<ul>
<li>Install Shopify script app (https://apps.shopify.com/script-editor)</li>
<li>Create discount code PREPAIDOFFER</li>
<li>Show Banner with prepaid discount PREPAIDOFFER</li>
<li>Create new payment script and copy code from this file to hide COD.</li>
</ul>

<pre>
Input.payment_gateways.each do |payment_gateway|
  if payment_gateway.name == "Cash on Delivery"
  else 
    payment_gateway.change_name(payment_gateway.name + " \n (Use coupon code 'PREPAIDOFFER' for 5% off on this payment method)");
  end 
end

Output.payment_gateways = Input.payment_gateways.delete_if do |payment_gateway|
  payment_gateway.name == "Cash on Delivery" && Input.cart.discount_code && Input.cart.discount_code.code == "PREPAIDOFFER"
end
</pre>
