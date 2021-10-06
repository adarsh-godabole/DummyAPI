<template>
  <div>
    <button @click="getdata()">Display All </button>
    <input type="text" v-model="id">
    <button @click="getsingledata()">Display One </button>
    <div v-show="displayall">
      <div v-bind:key="task.id" v-for="task in tasks">
        <p>{{task.id}}</p>
        <p>{{task.title}}</p>
      </div>
    </div>
    <div>
      {{result.id}}<br>
      {{result.title}}
    </div>
    <div class="add">
      <input type="text" name="" id="" v-model="nid">
            <input type="text" name="" id="" v-model="ntitle">
      <button @click=add()>ADD</button>
    </div>
  </div>
</template>
<script>
  export default {
    name: 'HelloWorld',
    data() {
      return {
        task:Object,
        tasks: Array,
        displayall: Boolean,
        id:String,
        result:String,
        nid:String,
        ntitle:String
      }
    },
    created() {
      this.id= '',
      this.ntitle=" ",
      this.nid=" "
    },
    methods: {
      async add()
      {
        const newtask=
        {
        id:this.nid,
        title:this.ntitle
        }
        const res = await fetch('https://jsonplaceholder.typicode.com/posts',
        {
          method:'POST',
          headers:{
            'Content-type':'application/json'
          },
          body:JSON.stringify(newtask)
        })

        const data = await res.json()

console.log(newtask.id);
        this.tasks.push(data)

      },
      async getsingledata() {
        this.displayall = false;
        const res = await fetch(`https://jsonplaceholder.typicode.com/posts/${this.id}`)
        const data = await res.json();
        this.result=data;
      },
      async getdata() {
        this.displayall = true;
        const res = await fetch('https://jsonplaceholder.typicode.com/posts')
        const data = await res.json()
        console.log(data);
        this.tasks = data
      }
    }
  }
</script>
<style scoped>
</style>
