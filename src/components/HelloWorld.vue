<template>
  <div id="app">
    <div>
      <b-navbar  toggleable="lg" type="dark" class="bgg text-center">
        <h1 >Music</h1>
      </b-navbar>
    </div>

    <div>
      <b-carousel
        id="carousel-fade"
        style="text-shadow: 0px 0px 2px #000"
        fade
        indicators
        img-width="1024"
        img-height="480"
      >
        <b-carousel-slide
          caption=""
          img-src="https://images.wallpaperscraft.com/image/violin_bw_violin_bow_121396_3840x2160.jpg"
        ></b-carousel-slide>
        <b-carousel-slide
          caption=""
          img-src="https://images.wallpaperscraft.com/image/headphones_bw_headset_120277_3840x2160.jpg"
        ></b-carousel-slide>
        <b-carousel-slide
          caption=""
          img-src="https://images.wallpaperscraft.com/image/headphones_books_education_121501_3840x2160.jpg"
        ></b-carousel-slide>
      </b-carousel>
    </div>

    <div class="container">
      <hr />
      <div class="row">
        <div class="col-md-3" v-for="item in products" :key="item">
          <b-card
            :img-src="item.image"
            img-alt="Image"
            img-top
            tag="article"
            style="max-width: 20rem"
            class="mb-2 my-3 text-center"
          >
            <h6 class="text-left" style="color: navy">{{ item.name }}</h6>
            <b-card-text class="text-left" style="color: orangered">
              ราคา {{ item.price }} THB.
            </b-card-text>

            <b-button href="#" variant="primary" @click="addCart(item)"
              >หยิบใส่ตะกร้า</b-button
            >
          </b-card>
        </div>
        <div class="col-md-8" v-if="carts != 0">
          <h4>
            ตะกร้าเพลง
            <i class="fa fa-shopping-cart"></i>
          </h4>
          <hr />
          <table class="table">
            <thead class="thead-dark">
              <tr>
                <th scope="col">ภาพ</th>
                <th scope="col">ชื่อ</th>
                <th scope="col">ราคา</th>
                <th scope="col">จำนวน</th>
                <th scope="col">ยอดรวม</th>
                <th scope="col">ลบ</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="product in carts" :key="product">
                <td>
                  <img
                    :src="product.image"
                    alt=""
                    width="80px"
                    height="100px"
                  />
                </td>
                <td>{{ product.name }}</td>
                <td>{{ product.price }}</td>
                <td>
                  <i
                    class="fa fa-minus qty-minus"
                    @click="minusQty(product)"
                  ></i>
                  {{ product.qty }}
                  <i class="fa fa-plus qty-plus" @click="plusQty(product)"></i>
                </td>
                <td>{{ product.total }}</td>
                <td>
                  <button @click="removeProduct(product)" class="btn-danger">
                    <i class="fa fa-trash"></i>
                  </button>
                </td>
              </tr>
              <!-- <button class="align-center">ซื้อสินค้า</button> -->
            </tbody>
          </table>
          <div>
            <h4 align="right">ยอดชำระเงิน {{ total() }} บาท</h4>

            <!-- <button class="checkoutCart" v-show="checkoutBool" @click="propagateCheckout()"> Checkout </button> -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Cart",
  data() {
    return {
      carts: [],
      pd1: 0,
      pd2: 0,
      pd3: 0,
      pd4: 0,
      pd5: 0,
      pd6: 0,
      pd7: 0,
      pd8: 0,
      products: [
        {
          id: 1,
          name: "Drake",
          price: 25,
          image:
            "https://is5-ssl.mzstatic.com/image/thumb/Music114/v4/22/fb/36/22fb36e7-386d-4ba8-0577-9975577f7c19/21UMGIM18577.rgb.jpg/300x300bb.webp",
          active: false,
        },
        {
          id: 2,
          name: "change-of-scenery-ii",
          price: 30,
          image:
            "https://is4-ssl.mzstatic.com/image/thumb/Music124/v4/b1/e6/33/b1e633cf-57ee-0d47-7d65-4365e41eca2d/886449048410.jpg/300x300bb.webp",
          active: false,
        },
        {
          id: 3,
          name: "youre-welcome",
          price: 45,
          image:
            "https://is4-ssl.mzstatic.com/image/thumb/Music124/v4/cd/52/05/cd520524-378f-2036-4eee-53d9a863311a/075679838162.jpg/300x300bb.webp",
          active: false,
        },
        {
          id: 4,
          name: "When You See Yourself",
          price: 35,
          image:
            "https://is3-ssl.mzstatic.com/image/thumb/Video114/v4/ed/d6/8c/edd68c85-7ae7-c601-f479-56575a8bf961/Job07da2b08-a59a-4f21-bfb3-babcee9b80a6-109603343-PreviewImage_PreviewImageIntermediate_preview_image_nonvideo_vfcs108015037-Time1614197854706.png/300x300bb.webp",
          active: false,
        },
        {
          id: 5,
          name: "NIRATIAS",
          price: 40,
          image:
            "https://is3-ssl.mzstatic.com/image/thumb/Music124/v4/0c/ee/55/0cee5518-58db-4ca9-ea14-38de5459ddfd/886448648000.jpg/300x300bb.webp",
          active: false,
        },
        {
          id: 6,
          name: "Poster Girl",
          price: 50,
          image:
            "https://is2-ssl.mzstatic.com/image/thumb/Music114/v4/0c/99/5e/0c995e45-c27b-60a8-b24b-fb7f23f67ac1/886449023707.jpg/300x300bb.webp",
          active: false,
        },
        {
          id: 7,
          name: " Mis Manos",
          price: 45,
          image:
            "https://is1-ssl.mzstatic.com/image/thumb/Music114/v4/6e/6d/00/6e6d00ce-9c1a-689c-24c4-80634a20ac52/886449097258.jpg/300x300bb.webp",
          active: false,
        },
        {
          id: 8,
          name: "Coming 2 America ",
          price: 39,
          image:
            "https://is5-ssl.mzstatic.com/image/thumb/Music114/v4/64/ca/d5/64cad5cb-a963-0eee-39df-1a2f6cb1cc65/21UMGIM16384.rgb.jpg/300x300bb.webp",
          active: false,
        },
      ],
    };
  },
  methods: {
    addCart: function (item) {
      var found = false;

      if (item.id == 1) {
        this.pd1 += 1;
        if (this.pd1 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (item.id == 2) {
        this.pd2 += 1;
        if (this.pd2 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (item.id == 3) {
        this.pd3 += 1;
        if (this.pd3 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (item.id == 4) {
        this.pd4 += 1;
        if (this.pd4 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (item.id == 5) {
        this.pd5 += 1;
        if (this.pd5 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (item.id == 6) {
        this.pd6 += 1;
        if (this.pd6 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (item.id == 7) {
        this.pd7 += 1;
        if (this.pd7 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      } else if (item.id == 8) {
        this.pd8 += 1;
        if (this.pd8 <= 1) {
          this.pushData(item);
        } else {
          found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      }
    },
    pushData(item) {
      this.carts.push({
        id: item.id,
        name: item.name,
        price: item.price,
        image: item.image,
        qty: 1,
        total: item.price,
      });
    },
    findIndex: function (item) {
      for (var i = 0; i < this.carts.length; i++) {
        if (this.carts[i].id == item.id) {
          return i;
        }
      }
      return -1;
    },
    minusQty: function (product) {
      product.qty -= 1;
      if (product.qty <= 1) {
        product.qty = 1;
      }
      product.total = product.price * product.qty;
    },
    plusQty: function (product) {
      product.qty += 1;
      product.total = product.price * product.qty;
    },
    removeProduct(product) {
      if (confirm("คุณต้องการลบหรือไม่ ?")) {
        var index = this.carts.indexOf(product);
        this.carts.splice(index, 1);
        if (product.id == 1) {
          this.pd1 = 0;
        } else {
          this.tea = 0;
        }
      }
    },
    total: function () {
      var sum = 0;
      this.carts.forEach(function (item) {
        sum += item.total;
      });
      return sum;
    },
  },
};
</script>
<style scoped>
.qty-minus {
  cursor: pointer;
  margin-right: 20px;
}
.qty-plus {
  cursor: pointer;
  margin-left: 20px;
}
.bgg {
  background-color: rgb(111, 184, 83);
}

/* .checkout-area table {
  margin: 0 auto;
  padding: 0.5em;
  width: 100%;
  max-width: 40em;
  text-align: left;
}
.checkout-area table th, .checkout-area table td {
  padding: 0 0.25em;
}
@media (max-width: 600px) {
  .checkout-area table th:nth-child(3), .checkout-area table td:nth-child(3) {
    display: none;
  }
} */
</style>