<template>
  <div class="note"
       :class="[classObject(note), {full: !grid}]"
  >
    <div class="note-header" :class="{ full: !grid}">
      <input class="inp_text_card"
             type="text"
             :readonly="readonly"
             :class="{'readonly': readonly === false}"
             v-model="copy.title"
      >
      <div class="controls">
        <i @click="touchInput" class="far"
           :class="{ 'fa-edit': readonly === true, 'fa-save': readonly === false }"></i>
        <i @click="removeNote(copy.id)" class="far fa-times-circle"></i>
      </div>
    </div>
    <div class="note-body">
      <input class="inp_text_card"
             type="text"
             :readonly="readonly"
             v-model="copy.descr"
             :class="{'readonly': readonly === false}" >
      <div class="note-bottom">
        <span>{{ copy.date }}</span>
        <div class="radio" :class="{ 'edit': readonly === false }" >
          <input type="radio" :id="'light'+copy.id"
                 value="light"
                 required
                 checked
                 v-model="copy.priority">
          <label :for="'light'+copy.id" >Light</label>
    
          <input type="radio" :id="'middleComp'+copy.id" value="middle"
                 v-model="copy.priority">
          <label :for="'middleComp'+copy.id">Middle</label>
    
          <input type="radio" :id="'highComp'+copy.id" value="high"
                 v-model="copy.priority">
          <label :for="'highComp'+copy.id">High</label>
        </div>
      </div>
      
    </div>
  </div>
</template>


<script>
export default {
    props: {
        note: {
            type: Object,
            required: true
        },
        grid: {
            type: Boolean,
            required: true
        }
    },
    created() {
        document.body.addEventListener('click', this.handleFocusOut);
        document.body.addEventListener('keyup', this.changeNote);
    },
    destroyed() {
        document.body.removeEventListener('click', this.handleFocusOut);
        document.body.removeEventListener('keyup', this.changeNote);
    },
    data () {
        return {
            readonly: true,
            copy: Object.assign({}, this.note)
        }
    },
    methods: {
        handleFocusOut(event) {
            if (!event.path.includes(this.$el)) {
                this.falseChange()
            }
        },
        removeNote (id) {
            this.$emit('remove', id)
        },
        classObject (note) {
            return `${note.priority}`
        },
        touchInput () {
            if (this.readonly === true) {
                this.readonly = false
            } else {
                this.trueChange()
            }
        },
        changeNote (event) {

            if (event.keyCode === 13) {
                if (this.readonly === false) {
                    this.trueChange()
                }
            } else if (event.keyCode === 27) {
                this.falseChange()
            }
        },
        falseChange() {
            this.copy.title = this.note.title
            this.copy.descr = this.note.descr
            this.copy.priority = this.note.priority
            
            this.readonly = true
        },
        trueChange() {
            this.note.title = this.copy.title
            this.note.descr = this.copy.descr
            this.note.priority = this.copy.priority
            this.note.date = new Date(Date.now()).toLocaleString()
            this.readonly = true
        }
    },
}
</script>


<style lang="scss">


</style>
