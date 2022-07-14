<template>
  <!-- Setting the Base Tag -->
  <div id="myshop">
    <!-- Image -->
    <img :src="image" alt="Image of Nike T-shirt" />

    <!-- info section -->
    <!--  Within this info -->
    <div id="infoSection">
      <!-- Current Tshirt Colors -->

      <ul v-for="(item, index) in items" :key="item.id">
        <!-- {{ item.name }} : -->
        <ul>
            <!-- Event listening achieved !  -->
          <div v-on:mouseover="changeImageOnHover(index)" :style="{ background: item.color }" id="colorCircle"></div>
        </ul>
      </ul>
      <!-- Colors -->
      <!-- Purchase Section -->
      <h2>Info Section</h2>
      <button>Add To Cart</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      image: "src/assets/red_nike_tshirt.png",
      //     We have our items array here so what we are going to do it loop through them and display
      items: [
        {
          id: 1,
          name: "Red T-Shirt",
          color: "red",
          image: "src/assets/red_nike_tshirt.png",
          price: 400,
          currentStockAvailable: 10,
        },
        {
          id: 2,
          name: "Black T-Shirt",
          color: "black",
          image: "src/assets/black_nike_tshirt.jpg",
          price: 400,
          currentStockAvailable: 10,
        },
      ],
    };
  },
 
  methods: {
    //   Function is triggered on hover 
     changeImageOnHover(index){
         console.log("index", index)
         this.image = this.items[index].image
         return this.items[index].image

    }
  },
};
</script>

<style>
#myshop {
  display: flex;
}
img {
  height: 200px;
  margin-right: 10px;
}
#infoSection {
  height: 100%;
  display: grid;
  padding: 10px;
}
button {
  background: #02afaf;
}
/* Lets change the cursor type on hover as well */
#colorCircle {
  width: 100px;
  height: 20px;
  border-radius: 30px;
  cursor: pointer;
  
}
</style>
