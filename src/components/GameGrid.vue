<template lang="html">
  <div class="grid" >
    <div v-for="(style, index) in boxStyles" :style="style"  v-on:click="clickSquare(index)">

    </div>
  </div>
</template>

<script>
export default {
  name: "game-grid",
  data() {
    return {
      boxStyles: [],
      player1: true,
      clickedSquares: {},
      p1Color: 'royalblue',
      p2Color: 'crimson'
    }
  },
  computed: {
    dynamicBoxStyles() {
      return this.boxStyles
    }
  },
  created(){
    const squares = {}
    const styles = []
    for(let i=1; i< 11; i++){
      for(let j=1; j<11; j++){
        const style = {
          'border': '1px solid black',
          'grid-column': `${i} / ${i+1}`,
          'grid-row': `${j} / ${j+1}`,
          'width': '100%',
          'height': '100%',
          'background-color': 'snow'
        }
        styles.push(style)
        squares[styles.length - 1] = true
      }
    }
    this.boxStyles = styles
    this.clickedSquares = squares
  },
  methods: {
    clickSquare(index) {
      console.log(index)
      if(this.clickedSquares[index] == true){
        if(this.player1){
          this.boxStyles[index]['background-color'] = this.p1Color
          // Left to right
          for(let i=index+10; i < 100 ;i+=10){
            // console.log(i, this.boxStyles[i]['background-color'])
            if(this.boxStyles[i]['background-color'] == 'snow'){
              i = 100;
            }else if(this.boxStyles[i]['background-color'] == this.p1Color){
              for(let j=i-10; j >= index+10; j-=10){
                this.boxStyles[j]['background-color'] = this.p1Color
              }
              i=100;
            }
          }
          // Right to left
          for(let i=index-10; i>0; i-=10){
            if(this.boxStyles[i]['background-color'] == 'snow'){
              i = -1;
            }else if(this.boxStyles[i]['background-color'] == this.p1Color){
              for(let j=i+10; j <= index-10; j+=10){
                this.boxStyles[j]['background-color'] = this.p1Color
              }
              i = -1;
            }
          }
          // Top to bottom
          for(let i=index+1; i%10 != 0; i++ ){
            if(this.boxStyles[i]['background-color'] == 'snow'){
              i = 99;
            }else if(this.boxStyles[i]['background-color'] == this.p1Color){
              for(let j=i-1; j >= index+1; j--){
                this.boxStyles[j]['background-color'] = this.p1Color
              }
              i=99;
            }
          }
          // Bottom to top
          for (let i=index-1; (i+1)%10 != 0; i--){
            if(this.boxStyles[i]['background-color'] == 'snow'){
              i = 0;
            }else if(this.boxStyles[i]['background-color'] == this.p1Color){
              for(let j=i+1; j <= index-1; j++){
                this.boxStyles[j]['background-color'] = this.p1Color
              }
              i=0;
            }
          }
          //Diagonal top to bottom, right to left
          for(let i=index-9; i%10 != 0 && i > 0; i-=9){
            if(this.boxStyles[i]['background-color'] == 'snow'){
               i = 109;
            } else if(this.boxStyles[i]['background-color'] == this.p1Color){
              for(let j=i+9; j <= index-9; j+=9){
                this.boxStyles[j]['background-color'] = this.p1Color
              }
              i=109;
            }
          }
         //Diagonal top to bottom, left to right
          for(let i=index+11; i%10 != 0 && i<100; i+=11){
            if(this.boxStyles[i]['background-color'] == 'snow'){
              i = 99;
            }else if(this.boxStyles[i]['background-color'] == this.p1Color){
              for(let j=i-11; j >= index+11; j-=11){
                this.boxStyles[j]['background-color'] = this.p1Color
              }
              i=99;
            }
          }
          //Diagonal bottom to top, left to right
          for(let i=index-11; (i+1)%10 != 0 && i>0; i-=11){
            if(this.boxStyles[i]['background-color'] == 'snow'){
              i = 11;
            }else if(this.boxStyles[i]['background-color'] == this.p1Color){
              for(let j=i+11; j <= index-11; j+=11){
                this.boxStyles[j]['background-color'] = this.p1Color
              }
              i=11;
            }
          }
          //Diagonal bottom to top, left to right
          for(let i=index+9; (i+1)%10 != 0 && i<100; i+=9){
            console.log(i)
            if(this.boxStyles[i]['background-color'] == 'snow'){
              i = 91;
            }else if(this.boxStyles[i]['background-color'] == this.p1Color){
              for(let j=i-9; j >= index+9; j-=9){
                this.boxStyles[j]['background-color'] = this.p1Color
              }
              i=91;
            }
           }
        } else {
          this.boxStyles[index]['background-color'] = this.p2Color
          //Left to right
          for(let i=index+10; i < 100 ;i+=10){
            // console.log(i, this.boxStyles[i]['background-color'])
            if(this.boxStyles[i]['background-color'] == 'snow'){
              i = 100;
            }else if(this.boxStyles[i]['background-color'] == this.p2Color){
              for(let j=i-10; j >= index+10; j-=10){
                this.boxStyles[j]['background-color'] = this.p2Color
              }
              i=100;
            }
          }
          // Right to left
          for(let i=index-10; i>0; i-=10){
            if(this.boxStyles[i]['background-color'] == 'snow'){
              i = -1;
            }else if(this.boxStyles[i]['background-color'] == this.p2Color){
              for(let j=i+10; j <= index-10; j+=10){
                this.boxStyles[j]['background-color'] = this.p2Color
              }
              i = -1;
            }
          }
          // Top to bottom
          for(let i=index+1; i%10 != 0; i++ ){
            if(this.boxStyles[i]['background-color'] == 'snow'){
              i = 99;
            }else if(this.boxStyles[i]['background-color'] == this.p2Color){
              for(let j=i-1; j >= index+1; j--){
                this.boxStyles[j]['background-color'] = this.p2Color
              }
              i=99;
            }
          }
          // Bottom to top
          for (let i=index-1; (i+1)%10 != 0; i--){
            if(this.boxStyles[i]['background-color'] == 'snow'){
              i = 0;
            }else if(this.boxStyles[i]['background-color'] == this.p2Color){
              for(let j=i+1; j <= index-1; j++){
                this.boxStyles[j]['background-color'] = this.p2Color
              }
              i=0;
            }
          }
          //Diagonal top to bottom, right to left
          for(let i=index-9; i%10 != 0 && i > 0; i-=9){
            if(this.boxStyles[i]['background-color'] == 'snow'){
               i = 109;
            } else if(this.boxStyles[i]['background-color'] == this.p2Color){
              for(let j=i+9; j <= index-9; j+=9){
                this.boxStyles[j]['background-color'] = this.p2Color
              }
              i=109;
            }
          }
         //Diagonal top to bottom, left to right
          for(let i=index+11; i%10 != 0 && i<100; i+=11){
            if(this.boxStyles[i]['background-color'] == 'snow'){
              i = 99;
            }else if(this.boxStyles[i]['background-color'] == this.p2Color){
              for(let j=i-11; j >= index+11; j-=11){
                this.boxStyles[j]['background-color'] = this.p2Color
              }
              i=99;
            }
          }
          //Diagonal bottom to top, left to right
          for(let i=index-11; (i+1)%10 != 0 && i>0; i-=11){
            if(this.boxStyles[i]['background-color'] == 'snow'){
              i = 11;
            }else if(this.boxStyles[i]['background-color'] == this.p2Color){
              for(let j=i+11; j <= index-11; j+=11){
                this.boxStyles[j]['background-color'] = this.p2Color
              }
              i= 11;
            }
          }
          //Diagonal bottom to top, left to right
          for(let i=index+9; (i+1)%10 != 0 && i<100; i+=9){
            console.log(i)
            if(this.boxStyles[i]['background-color'] == 'snow'){
              i = 91;
            }else if(this.boxStyles[i]['background-color'] == this.p2Color){
              for(let j=i-9; j >= index+9; j-=9){
                this.boxStyles[j]['background-color'] = this.p2Color
              }
              i=91;
            }
          }
        }
        this.clickedSquares[index] = false
        this.player1 = !this.player1
      }
    }
  }
}
</script>

<style lang="css" scoped>

.grid {
  display: grid;
  grid-template-rows: repeat(10, 1fr);
  grid-template-columns: repeat(10, 1fr);
  width: 500px;
  height: 500px;
  border: 1px solid black;
}
</style>
