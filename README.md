# hide-specific-category-product-in-shop-page
As ‘clothing’ is an example in the snippet below, be sure to use a product category slug that exists in your WooCommerce store.  Note that this will only work when you have your “Shop Page Display” option set to ‘Show Products’ under WooCommerce > Settings > Products > Display.  You will need to put this code in your theme’s functions.php file.

<?php
function custom_pre_get_posts_query( $q ) {

    $tax_query = (array) $q->get( 'tax_query' );

    $tax_query[] = array(
           'taxonomy' => 'product_cat',
           'field' => 'slug',
           'terms' => array( 'clothing' ), // Don't display products in the clothing category on the shop page.
           'operator' => 'NOT IN'
    );


    $q->set( 'tax_query', $tax_query );

}
add_action( 'woocommerce_product_query', 'custom_pre_get_posts_query' );

?>
