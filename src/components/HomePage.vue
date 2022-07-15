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
      <button v-on:click="addToCart"  :disabled="itemAvailable === false">Add To Cart</button>
    </div>

<!-- Shows the Cart icon togetehr with the Item count -->
    <div id="priceSection"> 
      <!-- img of cart-->
      <img :src="shoppingCart" alt="" srcset="" id="shopping_cart">
      <!-- count -->
      <div class="countElement"> {{ quantity }} </div>

    </div>

  </div>
</template>

<script>

// default is our object it contains options-> an example of an aoptions is data, methods, props, mounted 
export default {
    // Data Option
  data() {
    return {
      deactivateButton:true,
      image: "src/assets/red_nike_tshirt.png",
      shoppingCart:"src/assets/shopping_cart.svg",
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
      console.log(" add to cart has been clicked ")

      // Get the name of the selected item : 
      let nameOfItem = this.items[this.selectedItem.index].name
      
      // get the current item quantity 
      let quantityOfItem = 0

        //   Reduce the existing quantity form the items  - is the items in stock 
        if(this.items[this.selectedItem.index].currentStockAvailable > 0){
        this.items[this.selectedItem.index].currentStockAvailable -=1
        //    Add Item count
        this.quantity +=1     
        }
        else{
        // Hide deactivate the button
        //     if the items reaches 0 we deactivate the add to card button
         this.itemAvailable = !this.itemAvailable
        }
          let itemPurchaseObject = {
          'name':nameOfItem,
          'numberOfItem':this.quantity
        }

        // Add the item purchase to the itemsPurchased array
       this.itemsPurchased.push(itemPurchaseObject)
        console.log("Product => ",itemPurchaseObject)
           
    },
    // Set the currently selected item
    setCurrentItem(index){
      this.itemAvailable = true
              this.quantity = 0
         this.selectedItem.index = index
         this.image = this.items[index].image
         this.selectedItem.name = this.items[index].name
    },

    resetAll(){
      this.quantity = 0
        this.selectedItem.name=""
        this.selectedItem.index = -1
        if(this.itemsPurchased.length > 0 ){
          for(let i = 0;i < this.itemsPurchased.length;i++ ){
            this.itemsPurchased[i].name = ""
            this.itemsPurchased[i].numberOfItem =""
          }
        }
   }, 
  },
};
</script>

<style>
#myshop {
  display: flex;
}
/* .shopping_cart{

} */
.countElement{
  font-size:40px; 
  margin:auto;

}
#priceSection{
  display:flex;
  height:min-content; 

}
#shopping_cart{
    width:40px;
    height: 40px;
    margin-left: 20px;
    margin-right: 20px;
    padding:10px;
    background: #e2ce8c;
    border-radius: 30px;
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
