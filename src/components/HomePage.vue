<template>
  <!-- Setting the Base Tag -->
  <div id="myshop">
    <!-- Current Dynamic Image -->
    <img :src="image" alt="Image of Nike T-shirt" />

    <!-- info section --> 
    <div id="infoSection">
      <!-- Current Tshirt Colors -->
      <ul v-for="(item, index) in items" :key="item.id">
        <ul>
            <!-- Event listening achieved !  -->
          <div 
          v-on:mouseover="changeImageOnHover(index)" 
          v-on:click="setCurrentItem(index)"
          :style="{ background: item.color }" id="colorCircle"></div>
        </ul>
      </ul> 
      <!-- Purchase Section -->
      <h2>Info Section</h2>
      <h3>Selected Item : <span>{{ selectedItem.name }}</span></h3>
      <!-- 
          Button Features Onclick :
            - Add Item count
            - Reduce the existing quantity form the items 
            - if the items reaches 0 we deactivate the add to card button
       -->
       <button v-on:click="resetAll" id="resetButton">reset</button>

      <button v-on:click="addToCart" v-if="itemAvailable">Add To Cart</button>
    </div>
  </div>
</template>

<script>

// default is our object it contains options-> an example of an aoptions is data, methods, props, mounted 
export default {
    // Data Option
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
      quantity:0,
      selectedItem:{
          index:-1, // if value is negative that means it has not changed
          name:""
   },

      itemsPurchased:[],
      itemAvailable:true

    };
  },
//  Methods Options -> hosts our functions
  methods: {
    //   Function is triggered on hover 
     changeImageOnHover(index){
         if(this.selectedItem.index === -1){
         this.image = this.items[index].image
         this.selectedItem.name = ""
         }
         else{
              this.image = this.items[this.selectedItem.index].image
         }
        //  return this.items[this.selectedItem.index].image
    },
    
    addToCart(){ 
        //   Reduce the existing quantity form the items 
        if(this.items[this.selectedItem.index].currentStockAvailable >0){
        this.items[this.selectedItem.index].currentStockAvailable -=1
        //    Add Item count
        this.quantity +=1     
        }
        else{
            // Hide deactivate the button
        //     if the items reaches 0 we deactivate the add to card button
         this.itemAvailable = !this.itemAvailable
        }

           
    },
    // SEt the currently selected item
    setCurrentItem(index){
        this.selectedItem.index = index
         this.image = this.items[index].image
         this.selectedItem.name = this.items[index].name
    },
    resetAll(){
        this.selectedItem.name=""
        this.selectedItem.index = -1
   }, 
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
#resetButton{
    width:auto;
    margin:10px;
    background: #e90000;
    color: aliceblue;
    font-size: 16px;  
    font-weight:bold
}
</style>
