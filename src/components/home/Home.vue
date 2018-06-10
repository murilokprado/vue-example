<template>
    
  <div>
    <h1 class="center-pic" >{{ title }}</h1>

    <ul class="list-pic">
      <input type="search" class="filter" @input="filter = $event.target.value" placeholder="filter title"/>

      <li class="list-pic-item" v-for="pic of picFilter" :key="pic.url">
        <my-panel :title="pic.titulo">
          <img-responsive :url="pic.url" :title="pic.titulo"/>
          <my-button type="button" title="Remove" @buttonActive="remove(pic)" :confirmation="false" styleButton="warning"/>
        </my-panel>
      </li>

    </ul>
  </div>

</template>

<script>
import Panel from '../shared/panel/Panel.vue';
import ImageResponsive from '../shared/img-responsive/ImageResponsive.vue';
import Button from '../shared/button/Button.vue';

export default {
    components: {
      'my-panel': Panel,
      'img-responsive': ImageResponsive,
      'my-button': Button
    },
    data() {
      return {
        title: "Vue Example",
        pics: [],
        filter: ''
      }
    },
    created() {
      let promise = this.$http.get('http://localhost:3000/v1/fotos')
        .then(res => res.json())
        .then(pics => this.pics = pics, err => console.log(err));
    },
    computed: {
      picFilter() {
        if(this.filter) {
          let exp = new RegExp(this.filter.trim(), 'i');
          return this.pics.filter(pic => exp.test(pic.titulo));
        } else {
          return this.pics;
        }
      }
    },
    methods: {
      remove(pic) {
        alert("REMOVE - " + pic.titulo);
      }
    }
}
</script>

<style>

.center-pic {
  text-align: center;
}

.list-pic {
  list-style: none;
}

.list-pic .list-pic-item {
  display: inline-block;
}

.filter {
  display: block;
  width: 100%;
}

</style>
