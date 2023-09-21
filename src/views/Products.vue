<script setup>
import axios from "axios";
import {ref, onBeforeMount} from 'vue';

let products = ref([]);

onBeforeMount(() => {
    getProducts();
});

async function getProducts(){
    let res = await axios.get('https://dummyjson.com/products');
    products.value = res.data;
}
</script>
<template>
    <main class="main">
        <div class="page-header text-center" style="background-image: url('assets/images/page-header-bg.jpg')">
            <div class="container-fluid">
                <h1 class="page-title">Products<span>Shop</span></h1>
            </div><!-- End .container-fluid -->
        </div><!-- End .page-header -->
        <nav aria-label="breadcrumb" class="breadcrumb-nav mb-2">
            <div class="container-fluid">
                <ol class="breadcrumb">
                    <li class="breadcrumb-item"><a href="index.html">Home</a></li>
                    <li class="breadcrumb-item"><a href="#">Shop</a></li>
                    <li class="breadcrumb-item active" aria-current="page">Products</li>
                </ol>
            </div><!-- End .container-fluid -->
        </nav><!-- End .breadcrumb-nav -->

        <div class="page-content">
            <div class="container-fluid">
                <div class="toolbox">
                    <div class="toolbox-left">
                        <div class="toolbox-info">
                            Showing <span>{{ products.limit }} of {{ products.total }}</span> Products
                        </div><!-- End .toolbox-info -->
                    </div><!-- End .toolbox-left -->

                    <div class="toolbox-center">
                        
                    </div><!-- End .toolbox-center -->

                    <div class="toolbox-right">
                        <div class="toolbox-sort">
                            <label for="sortby">Sort by:</label>
                            <div class="select-custom">
                                <select name="sortby" id="sortby" class="form-control">
                                    <option value="popularity" selected="selected">Most Popular</option>
                                    <option value="rating">Most Rated</option>
                                    <option value="date">Date</option>
                                </select>
                            </div>
                        </div><!-- End .toolbox-sort -->
                    </div><!-- End .toolbox-right -->
                </div><!-- End .toolbox -->

                <div class="products">
                    <div class="row">
                        <div v-for="(product,index) in products.products" :key="index" class="col-6 col-md-4 col-lg-4 col-xl-3 col-xxl-2">
                            <div class="product">
                                <figure class="product-media">
                                    <span class="product-label label-new">{{ product.brand }}</span>
                                    <router-link :to="`/product-details/${ product.id }`">
                                        <img :src="product.thumbnail" alt="Product image" class="product-image">
                                    </router-link>

                                    <div class="product-action-vertical">
                                        <a href="#" class="btn-product-icon btn-wishlist btn-expandable"><span>add to wishlist</span></a>
                                    </div><!-- End .product-action -->

                                    <div class="product-action action-icon-top">
                                        <a href="#" class="btn-product btn-cart"><span>add to cart</span></a>
                                        <a href="popup/quickView.html" class="btn-product btn-quickview" title="Quick view"><span>quick view</span></a>
                                        <a href="#" class="btn-product btn-compare" title="Compare"><span>compare</span></a>
                                    </div><!-- End .product-action -->
                                </figure><!-- End .product-media -->

                                <div class="product-body">
                                    <div class="product-cat">
                                        <a href="#">{{ product.category  }}</a>
                                    </div><!-- End .product-cat -->
                                    <h3 class="product-title"><a href="product.html">{{ product.title }}</a></h3><!-- End .product-title -->
                                    <div class="product-price">
                                        ${{ product.price }}
                                    </div><!-- End .product-price -->
                                    <div class="ratings-container">
                                        <div class="ratings">
                                            <div class="ratings-val" style="width: 0%;"></div><!-- End .ratings-val -->
                                        </div><!-- End .ratings -->
                                        <span class="ratings-text">( 0 Reviews )</span>
                                    </div><!-- End .rating-container -->

                                    <div class="product-nav product-nav-dots">
                                        <a href="#" style="background: #cc9966;"><span class="sr-only">Color name</span></a>
                                        <a href="#" class="active" style="background: #ebebeb;"><span class="sr-only">Color name</span></a>
                                    </div><!-- End .product-nav -->
                                </div><!-- End .product-body -->
                            </div><!-- End .product -->
                        </div>
                    </div>

                </div><!-- End .products -->

            </div><!-- End .container-fluid -->
        </div><!-- End .page-content -->
    </main><!-- End .main -->
</template>
