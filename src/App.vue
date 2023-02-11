<script>
export default {
  data() {
    return {
      text: ``,
      uniqueChar: null
    }
  },
  methods: {
    check() {
      //remove punctuation marks
      this.text.replaceAll(/[.,\/#!$%\^&\*;:"{}=\-_`~()]/g, "")

      //converting text into an array by spaces, or a dot, or tape feed
      let textArr = this.text.split(/[.\s\n]/)

      //discard empty values
      textArr = textArr.filter((textItem) => !!textItem)

      //create a new array that contains arrays of word symbols
      let charArr = textArr.map(textItem => textItem = textItem.split(''))

      let resultArr = []

      //sort through the array with words and the array of letters of this word
      //find the number of found letters in the word
      //check whether the length is equal to 1, if so, write the value in the array, if not, then search further
      textArr.forEach((textItem, textIndex) => {
        charArr[textIndex].every(item => {
          let checkValue = textItem.match(new RegExp(`${item}`, 'g'))

          if (checkValue && checkValue.length === 1) {
            resultArr.push(...checkValue)
            return false
          } else {
            return true
          }
        })
      })

      //create a string from an array of letters
      let newArrText = resultArr.join('')

      //find a unique symbol using the same search method as above
      resultArr.every(item => {
        let checkValue = newArrText.match(new RegExp(`${item}`, 'g'))

        if (checkValue && checkValue.length === 1) {
          this.uniqueChar = checkValue
          return false
        } else {
          return true
        }
      })
    }
  }
}
</script>

<template>
  <main>
    <div class="wrapper">
      <textarea v-model="text" class="textarea">
      </textarea>

      <div>
        <button @click="check" class="btn">Check</button>
      </div>

      <div v-if="uniqueChar" class="text">
        Unique char: {{ uniqueChar[0] }}
      </div>
    </div>
  </main>
</template>

<style scoped>
</style>
