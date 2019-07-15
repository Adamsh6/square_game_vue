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
      clickedSquares: {}
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
      if(this.clickedSquares[index] == true){
        if(this.player1){
          this.boxStyles[index]['background-color'] = "blue"
          for(let i=index+10; i < 100 ;i+=10){
            // console.log(i, this.boxStyles[i]['background-color'])
            if(this.boxStyles[i]['background-color'] == 'snow'){
              console.log('no effect')
              i = 100;
            }else if(this.boxStyles[i]['background-color'] == 'blue'){
              console.log('found a blue')
              for(let j=i-10; j >= index+10; j-=10){
                console.log(j)
                // console.log(j, this.boxStyles[j]['background-color'])
                this.boxStyles[j]['background-color'] = 'blue'
              }
              i=100;
            }
          }
        } else {
          this.boxStyles[index]['background-color'] = "red"
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
