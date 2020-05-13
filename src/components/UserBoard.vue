<template>
  <div class="container">
    <h1>Welcome to {{msg}} page</h1>
    <p>sort by</p>
    <div class="switch switch--horizontal">
      <input v-model="sortedBy" value="status" id="radio-a" type="radio" name="first-switch"/>
      <label for="radio-a">status</label>
      <input v-model="sortedBy" value="rating" id="radio-b" type="radio" name="first-switch" checked="checked"/>
      <label for="radio-b">rating</label><span class="toggle-outside"><span class="toggle-inside"></span></span>
    </div>
    <div class="search">
      <input v-model="query" type="text" v-html="query" class="show__search">
      <input @click="searchShows" class="btn btn--search" type="button" value="search">
    </div>
    <table>
      <thead>
        <tr>
          <td>Show name</td>
          <td>Language</td>
          <td>Genres</td>
          <td>Status</td>
          <td>Rating</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in shows">
          <td>{{item.show.name}}</td>
          <td>{{item.show.language}}</td>
          <td> {{ item.show.genres.join(', ') }}</td>
          <td>{{item.show.status}}</td>
          <td>{{item.show.rating.average}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        msg: 'TV shows',
        shows: null,
        query: 'girls',
        sortedBy: 'rating'
      }
    },
    methods: {
      searchShows() {
        this.$root.$emit('loader', true);
        this.$http.get(`http://api.tvmaze.com/search/shows?q=${this.query}`,
          { crossdomain: true
          })
          .then(response => { this.shows = response.data })
          .then(() => this.$root.$emit('loader', false))
          .then(() => this.sortByRating())

      .catch(error => console.error(error.response))
      },
      sortByRating() {
        this.shows.sort(function(a, b) {
          return b.show.rating.average - a.show.rating.average;
        });
      },
      sortByStatus() {
        let res = [];
        let sortByGroup = {
            group1: [],
            group2: [],
            group3: [],
          };

        this.shows.forEach((item) => {
          switch (item.show.status) {
            case 'Running':
              sortByGroup.group1.push(item);
              break;
            case 'To Be Determined':
              sortByGroup.group2.push(item);
              break;
            case 'Ended':
              sortByGroup.group3.push(item);
              break;
          }
        });

        res= [...sortByGroup.group1, ...sortByGroup.group2, ...sortByGroup.group3];
        this.shows = res;
      }
    },
    created() {
      this.searchShows('girls');
    },
    watch: {
      sortedBy: function (val) {
        val === 'status' ? this.sortByStatus() : this.sortByRating();
      },
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
  p {
    font-size: 32px;
    margin: 25px 0 15px;
  }
  table {
    border: 1px solid rgba(102, 102, 102, 0.2);
    width: 100%;
  }
  thead td {
    font-weight: 600;
  }
  td {
    padding: 5px;
    width: 20%;
  }
  .container {
    padding: 20px 0;
    max-width: 1024px;
    margin: 0 auto;
  }
  .search {
    margin: 10px auto 20px;
  }
  .show__search {
    outline: none;
    width: 100%;
    max-width: 220px;
    border: 1px solid rgba(102, 102, 102, 0.2);
    border-radius: 5px;
    padding: 10px;
    font-size: 18px;
    font-weight: 300;
    vertical-align: bottom;
  }
  .switch {
    margin: 4rem auto;
  }
  /* main styles */
  .switch {
    width: 24rem;
    position: relative;
  }
  .switch input {
    position: absolute;
    top: 0;
    z-index: 2;
    opacity: 0;
    cursor: pointer;
  }
  .switch input:checked {
    z-index: 1;
  }
  .switch input:checked + label {
    opacity: 1;
    cursor: default;
  }
  .switch input:not(:checked) + label:hover {
    opacity: 0.5;
  }
  .switch label {
    color: #fff;
    opacity: 0.33;
    transition: opacity 0.25s ease;
    cursor: pointer;
  }
  .switch .toggle-outside {
    height: 100%;
    border-radius: 2rem;
    padding: 0.25rem;
    overflow: hidden;
    transition: 0.25s ease all;
  }
  .switch .toggle-inside {
    border-radius: 5rem;
    background: #35495d;
    position: absolute;
    transition: 0.25s ease all;
    top: 50%;
    transform: translateY(-50%);
  }
  .switch label {
    color: #666666;
  }
  .switch--horizontal {
    width: 18rem;
    height: 2rem;
    margin: 0 auto 30px;
    font-size: 0;
  }
  .switch--horizontal input {
    height: 3rem;
    width: 6rem;
    left: 6rem;
    margin: 0;
  }
  .switch--horizontal label {
    font-size: 1.5rem;
    line-height: 3rem;
    display: inline-block;
    width: 6rem;
    height: 100%;
    margin: 0;
    text-align: center;
  }
  .switch--horizontal label:last-of-type {
    margin-left: 6rem;
  }
  .switch--horizontal .toggle-outside {
    background: #41b883 ;
    position: absolute;
    width: 6rem;
    left: 6rem;
  }
  .switch--horizontal .toggle-inside {
    height: 1.75rem;
    width: 1.75rem;
  }
  .switch--horizontal input:checked ~ .toggle-outside .toggle-inside {
    left: 0.55rem;
  }
  .switch--horizontal input ~ input:checked ~ .toggle-outside .toggle-inside {
    left: 4.25rem;
  }
  .switch--vertical {
    width: 12rem;
    height: 6rem;
  }
  .switch--vertical input {
    height: 100%;
    width: 3rem;
    right: 0;
    margin: 0;
  }
  .switch--vertical label {
    font-size: 1.5rem;
    line-height: 3rem;
    display: block;
    width: 8rem;
    height: 50%;
    margin: 0;
    text-align: center;
  }
  .switch--vertical .toggle-outside {
    background: #fff;
    position: absolute;
    width: 3rem;
    height: 100%;
    right: 0;
    top: 0;
  }
  .switch--vertical .toggle-inside {
    height: 2.5rem;
    left: 0.25rem;
    top: 0.25rem;
    width: 2.5rem;
  }
  .switch--vertical input:checked ~ .toggle-outside .toggle-inside {
    top: 0.25rem;
  }
  .switch--vertical input ~ input:checked ~ .toggle-outside .toggle-inside {
    top: 3.25rem;
  }
  .switch--no-label label {
    width: 0;
    height: 0;
    visibility: hidden;
    overflow: hidden;
  }
  .switch--no-label input:checked ~ .toggle-outside .toggle-inside {
    background: rgba(0,0,0,0.2);
    border: 1px solid rgba(0,0,0,0.2);
  }
  .switch--no-label input ~ input:checked ~ .toggle-outside {
    background: #fff;
  }
  .switch--no-label input ~ input:checked ~ .toggle-outside .toggle-inside {
    background: #2ecc71;
  }
  .switch--no-label.switch--vertical {
    width: 3rem;
  }
  .switch--no-label.switch--horizontal {
    width: 6rem;
  }
  .switch--no-label.switch--horizontal input,
  .switch--no-label.switch--horizontal .toggle-outside {
    left: 0;
  }
  .switch--expanding-inner input:checked + label:hover ~ .toggle-outside .toggle-inside {
    height: 2.5rem;
    width: 2.5rem;
  }
  .switch--expanding-inner.switch--horizontal input:hover ~ .toggle-outside .toggle-inside {
    width: 3.5rem;
  }
  .switch--expanding-inner.switch--horizontal input:hover ~ input:checked ~ .toggle-outside .toggle-inside {
    left: 2.25rem;
  }
  .switch--expanding-inner.switch--vertical input:hover ~ .toggle-outside .toggle-inside {
    height: 3.5rem;
  }
  .switch--expanding-inner.switch--vertical input:hover ~ input:checked ~ .toggle-outside .toggle-inside {
    top: 2.25rem;
  }
  /* mixin */

</style>
