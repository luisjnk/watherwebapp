<template>
   <div :class="typeaheadState">
        <div class="typeahead__toggle" ref="toggle" @mousedown.prevent="toogle">
            <input type="text" class="typeahead__search" ref="search"

                v-model="search"
                
                @focus="onFocus"

                @blur="onBlur"

                @keydown.esc="onEscape"

                @keydown.down="onDownKey"

                @keydown.up="onUpKey"

                @keydown.enter="onEnterKey"

                v-on:keyup="keymonitor" 
            >

            <span class="typeahead__text" red="text">{{displayText}}</span>
        </div>
   
   <ul class="typeahead__list" v-if="open">
        <li class="typeahead__item" v-for="(option, index) in filteredOptions" :key="index">
            <a class="typeahead__link" @mousedown.prevent="select(option)"
              :class="[selectIndex === index ? 'typeahead__active':'']"
            > {{option.name}} {{option.country}} </a>
        </li>
   </ul>
     <main class="main-content">
     
    <cardweather
       v-for="(day,index) in dayList"
       key="Index"
       :day="day"
       :cityName="cityName"
       :country="country"></cardweather>
  </main>
 </div>  
</template>

<script type="text/javascript">
import axios from 'axios'
import Cardweather from './Cardweather'
import moment from 'moment'

export default {
  components: {
    Cardweather
  },
  data () {
    return {
      open: false,
      selectIndex: 0,
      displayText: 'Please Insert  your city, for search the weathers',
      search: '',
      Id: 0,
      options: [],
      count: 0,
      dayList: [],
      cityName: '',
      country: ''
    }
  },
  watch: {
    Id: function (val) {
      if (val !== 0) {
        this.getWeathers
      }
    }
  },
  computed: {
    typeaheadState () {
      return this.open ? 'typeahead typeahead__open' : 'typeahead'
    },
    filteredOptions () {
      const exp = new RegExp(this.search, 'i')
      return this.options.filter((option) => {
        return (exp.test(option.id) || exp.test(option.name))
      })
    },
    requestOptions () {
      console.log(process.env.APIURL)
      axios.get(process.env.APIURL + this.search)
        .then(response => {
          this.options = []
          var newoptions = []
          var cities = response.data.message
          cities.forEach(function (city) {
            newoptions.push(city)
          })
          this.options = newoptions
        })
        .catch(e => {
          console.log(e)
        })
    },
    getWeathers () {
      console.log(this.Id)
      axios.get(process.env.APIURL + `weather/` + this.Id)
        .then(response => {
          this.count = response.data.message.body.cnt
          this.cityName = response.data.message.body.city.name
          this.country = response.data.message.body.city.country
          var days = response.data.message.body.list
          days.forEach(function (day) {
            var date = new Date(day.dt * 1000)
            day.dt = moment(date).format('DD/MM/YYYY')
          })
          this.dayList = days
          console.log(this.dayList)
        })
        .catch(e => {
          console.log(e)
        })
    }
  },
  methods: {
    onDownKey () {
      if (this.filteredOptions.length - 1 > this.selectIndex) {
        this.selectIndex++
      }
    },
    onUpKey () {
      if (this.filteredOptions.length - 1 > this.selectIndex) {
        this.selectIndex--
      }
    },
    onEnterKey () {
      const option = this.filteredOptions[this.selectIndex]
      if (option) {
        this.select(option)
      }
    },
    select (option) {
      this.displayText = option.name
      this.$emit('input', (option.id))
      this.Id = option.id
      this.$refs.search.blur()
    },
    toogle (e) {
      if (e.target === this.$refs.toogle ||
         e.target === this.$refs.search ||
         e.target === this.$refs.text) {
        if (this.open) {
          if (e.target !== this.$refs.search &&
             e.target !== this.$refs.text) {
            this.$refs.search.blur()
          }
        } else {
          this.$refs.search.focus()
        }
      }
    },
    onFocus () {
      this.open = true
    },
    onBlur () {
      this.search = ''
      this.open = false
    },
    onEscape () {
      this.$refs.search.blur()
    },
    keymonitor () {
      if (this.search.length > 4) {
        this.requestOptions
      }
    },
    getSelectedId () {
      return this.Id
    }
  }
}

</script>


<style type="text/css">
    .typeahead {

        border-radius: 12px;

        border: 1px  #ccc;

        position: relative;

        z-index: 1;

        background-color: #2196f3;

        width: 100%;

        font-size: 20px;
    }

    .typeahead__open {
       border: 1px solid #41B883;
    }
    .typeahead__open .typeahead__text {
        color: #999;

        opacity: 0.4;
    }
    .typeahead__toggle {
        position: relative;

        z-index: 1;

        width: 100%;
    }

   .typeahead__search {

        position: absolute;

        top: 0;

        left: 0;

        line-height: 1em;

        font-size: 1em;

        padding: 10px;

        width: 100%;

        display: block;

        cursor: text;

        background: transparent;

        border: none;

        outline: none;

        z-index: 2;

   } 

   .typeahead__text {

        min-height: 36px;

        font-size: 1em;

        line-height: 1em;

        padding: 10px;

        display: inline-block;

        position: relative;

        z-index: 3;
   }

   .typeahead__list {

       margin: 0;

       padding: 0;
   }

   .typeahead__item {

       display: block;

       border: top 1px solid #f4f4f4;
   
   }

   .typeahead__link { 

       display: block;

       padding: 10px;

       line-height: 1em;

       font-size: 1em;

       cursor: pointer;
   }
 .typeahead__active {
       background: #41B883;

       color: #fff;
 }  


</style>
