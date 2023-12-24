<template>
  <div class="home">
    <ul>
      <li><span class="title">タイトル</span><span class="priority">優先度</span></li>
    </ul>
    <ul v-if="hasMemos">
      <li v-for="memo in memos" :key="memo.id">
        <router-link :to="{ name: 'edit', params: { id: memo.id }}">
          <div class="title"> {{ memo.title }} </div>
          <div class="priority" v-if="memo.priority == 'high'">高</div>
          <div class="priority" v-if="memo.priority == 'during'">中</div>
          <div class="priority" v-if="memo.priority == 'small'">小</div>
          <div class="priority" v-if="memo.priority == ''">なし</div>
        </router-link>
      </li>
    </ul>
    <p v-else>タスクはありません</p>
  </div>
</template>

<style scoped>

ul{
  margin: 0;
  padding: 0;

}

li{
  list-style: none;
  border-bottom: 1px solid #ccc;
  padding-bottom:10px;
  margin-bottom: 10px;
}

li a{
  color: #999;
  text-decoration: none;
}

.title {
  display: block;
  text-align: left;
  justify-content:flex-start;
}


.priority{
  display: block;  
  text-align: right;
  justify-content:flex-end;
}

</style>

<script>
export default {
  name: 'HomeView',
  computed: {
    hasMemos() {
      return this.$store.getters.getCount
    },
    memos() {
      return this.$store.getters.getAll
    }
  }
}
</script>
