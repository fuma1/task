<template>
    <MemoForm v-if="memo" :memo="memo" />
    <p v-else>指定されたタスクはありません</p>
</template>



<script>
import MemoForm from '@/components/MemoForm.vue'
export default {
    name: 'EditView',
    components: {
        MemoForm
    },
    computed: {
        memo() {
            const id = parseInt(this.$route.params.id)
            return this.$store.getters.getMemoById(id)
        }
    }
}
</script>
