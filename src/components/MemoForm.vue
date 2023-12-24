<template>
    <div><input type="text" v-model="title" placeholder="タイトル"></div>
    <div>
        <label for="priority-select">優先度：</label>
        <select name="priority" v-model="priority">
            <option value="high">高</option>
            <option value="during">中</option>
            <option value="small">小</option>
        </select>
    </div>
    <div><textarea v-model="content" placeholder="内容"></textarea></div>
    
    <div class="center">
        <button @click="save">保存</button>
        <button @click="remove" v-if="memo.id">削除</button>
    </div>
</template>

<script>
export default {
    name: "MemoForm",
    props: [
        'memo'
    ],
    data() {
        return {
            title: this.memo.title,
            content: this.memo.content,
            priority: this.memo.priority
        }
    },
    methods: {
        save() {
            let memo = {
                title: this.title,
                content: this.content,
                priority: this.priority
            }
            if (this.memo.id) {
                memo.id = this.memo.id
            }
            this.$store.commit('save', memo)
            this.$router.push('/')
        },
        remove() {
            this.$store.commit('delete', this.memo.id)
            this.$router.push('/')
        }
    }
}
</script>

<style scoped>
label {
  font-family: sans-serif;
  font-size: 1rem;
  padding-right: 10px;
}
select {
  font-size: 0.9rem;
  padding: 2px 5px;
}
div {
    margin-bottom: 10px;
}
input [type=text] {
    width:100%;
}
textarea {
    width: 100%;
    height: 30em;
}
button {
    width:5em;
    margin: 3px;
}
.center {
    text-align: center;
}
</style>