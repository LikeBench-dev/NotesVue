<template>
  <div class="new-note">
    
    <label>Title</label>
    <input type="text" v-model="note.title">
  
    <priority :note="note"/>
    
    <label>Description</label>
    <textarea v-model="note.descr"></textarea>
    
    <button class="btn btnPrimary" @click="addNote">New Note</button>
  </div>
</template>

<script>
import priority from '@/components/Priority.vue'
export default {
    components: {
        priority
    },
    props: {
        note: {
            type: Object,
            required: true
        }
    },
    methods: {
        addNote() {
            this.$emit('addNote', this.note)
        }
    }
}
</script>

<style lang="scss" >
.new-note {
  text-align: center;
}
.btn {
  margin: 20px 0;
}

</style>
