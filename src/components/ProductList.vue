<template>
  <section id="header">
    <div class="wrapper">
      <div class="header-con">
        <h2>Shopping App</h2>
        <button @click="showCart">My Cart</button>
      </div>
    </div>
  </section>
  <section id="homepage">
    <div class="wrapper">
      <div class="homepage-con">
        <h2>Product List</h2>
        <div class="product-widget-con">
          <div
            class="product-widget"
            v-for="(product, index) in productList"
            :key="index"
          >
            <img src="../assets/img/Product_Image.jpg" alt="Image" />
            <div class="product-details">
              <div class="product-header">
                <h4>{{ product.name }}</h4>
                <p>
                  <span>₱{{ product.price }}</span>
                </p>
              </div>
              <div class="product-desc-con">
                <p>Description:</p>
                <p>{{ product.description }}</p>
              </div>
              <button @click="addToCart(index)">
                <i class="bi bi-cart-plus"></i>
                <span>ADD TO CART</span>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
  <div class="backdrop" v-if="showCartSection">
    <Cart :cart="cart" @close-cart="closeCart" />
  </div>
</template>
  
  <script>
import Cart from "./CartView.vue";

export default {
  data() {
    return {
      productList: [
        {
          name: "Book",
          description:
            "A description summarizes a book's content to give readers a glimpse into what the book is about.",
          price: 100,
        },
        {
          name: "Pencil",
          description:
            "A pencil is a writing utensil with a graphite lead embedded in a wooden shaft.",
          price: 5,
        },
        {
          name: "Marker",
          description: "A marker is an ink-filled pen with a wide tip.",
          price: 15,
        },
        {
          name: "Bond Paper",
          description:
            "It is an uncoated stock that is used for writing, drawing, and of course printing things like letterhead and business documents.",
          price: 1,
        },
        {
          name: "Eraser",
          description:
            "Eraser is a piece of rubber or other material used to rub out marks made by ink, pencil, or chalk.",
          price: 5,
        },
        {
          name: "White Board",
          description:
            "A white board with a smooth, white surface, often fixed to a wall, on which you can write and draw using special pens.",
          price: 20,
        },
        {
          name: "Ballpen",
          description:
            "A pen that has a small metal ball as the point of transfer of ink to paper.",
          price: 15,
        },
        {
          name: "Colored Paper",
          description:
            "Colored papers are typically uniformly tinted with pigments or dye during the manufacturing process.",
          price: 2,
        },
      ],
      cart: [],
      showCartSection: false,
    };
  },
  components: {
    Cart,
  },
  methods: {
    showCart() {
      this.showCartSection = true;
    },
    closeCart() {
      this.showCartSection = false;
    },
    addToCart(index) {
      let existingItem = this.cart.find(
          (item) => item.name == this.productList[index].name
        ),
        item = this.productList[index];

      existingItem
        ? existingItem.quantity++
        : this.cart.push({
            name: item.name,
            description: item.description,
            price: item.price,
            quantity: 1,
          });

      successOrder("Product Successfuly Added.");
    },
  },
};
</script>
  
<style scoped>
body {
  background: #fff;
}

.backdrop {
  overflow: auto;
  top: 69px;
  position: fixed;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
}

p span {
  color: #15803d;
  font-weight: 500;
}

#header {
  z-index: 9;
  position: fixed;
  width: 100%;
  filter: drop-shadow(0 4px 3px rgb(0 0 0 / 0.07))
    drop-shadow(0 2px 2px rgb(0 0 0 / 0.06));
  background: #f43f5e;
}

#header .wrapper {
  max-width: 1440px;
  width: 100%;
}

#header h2 {
  color: #ffffff;
  font-weight: 700;
}

#header .header-con {
  padding: 20px 0;
  display: flex;
  justify-content: space-between;
}

#header .header-con button {
  border: none;
  background: transparent;
  color: #ffffff;
  font-weight: 500;
  transition: 0.2s;
  cursor: pointer;
}

#header .header-con button:hover {
  color: #fecdd3;
}

#homepage .homepage-con {
  display: flex;
  flex-direction: column;
  gap: 30px;
  padding: 150px 0;
}

#homepage .homepage-con h2 {
  text-align: center;
  font-size: 28px;
  padding-bottom: 10px;
  border-bottom: 1px solid #222222;
}

#homepage .homepage-con .product-widget-con {
  display: flex;
  flex-wrap: wrap;
  column-gap: 25px;
  justify-content: center;
  row-gap: 40px;
}

#homepage .wrapper {
  max-width: 1440px;
  width: 100%;
}

#homepage .product-widget {
  background: #ffffff;
  border-radius: 10px;
  filter: drop-shadow(0 10px 8px rgb(0 0 0 / 0.04))
    drop-shadow(0 4px 3px rgb(0 0 0 / 0.1));
}

#homepage .product-widget img {
  width: 300px;
  display: block;
  border-radius: 10px 10px 0 0;
}

#homepage .product-desc-con p:first-child {
  font-size: 14px;
  font-weight: 600;
  margin-bottom: 5px;
}

#homepage .product-details .product-header {
  display: flex;
  justify-content: space-between;
  margin: 10px 0 20px 0;
}

#homepage .product-details p {
  font-size: 14px;
}

#homepage .product-details h4 {
  font-size: 20px;
  font-weight: 400;
  line-height: 1em;
}

#homepage .product-desc-con p:last-child {
  font-size: 12px;
  height: 50px;
  overflow: auto;
}

p::-webkit-scrollbar {
  width: 0;
}

#homepage .product-details {
  word-wrap: break-word;
  max-width: 300px;
  padding: 20px;
}

#homepage .product-details button {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  margin-top: 20px;
  border: none;
  border-radius: 10px;
  color: #ffffff;
  font-weight: 600;
  background: #f43f5e;
  filter: drop-shadow(0 10px 8px rgb(0 0 0 / 0.04))
    drop-shadow(0 4px 3px rgb(0 0 0 / 0.1));
  font-size: 14px;
  padding: 20px 40px;
  width: 100%;
  transition: 0.2s;
  cursor: pointer;
}

#homepage .product-details button:hover {
  background: #e11d48;
}
</style>