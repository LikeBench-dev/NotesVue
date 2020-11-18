<template>

  <div class="wrapper">
    
    <div class="wrapper-content">
      <section>
        <div class="container">
          
          <!--  message-->
          <message v-if="message" :message="message"/>
          
          <!--  new note-->
          <newNote :note="note" @addNote="addNote"/>
          
          <!-- main title-->
          <div class="note-header" style="margin: 30px 0">
          
<!--            title-->
            <h1>{{ title }}</h1>
            
<!--            search-->
            <search
                    :value="search"
                    placeholder="Find your note"
                    @search="search = $event"/>
            
<!--            icons controls-->
            <div class="icons">
              <svg :class="{ active: grid }"
                   @click="grid = true"
                   style="cursor: pointer;"
                   xmlns="http://www.w3.org/2000/svg"
                   width="24"
                    height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
              <svg :class="{ active: !grid }"
                   @click="grid = false"
                   style="cursor: pointer;"
                   xmlns="http://www.w3.org/2000/svg" width="24"
                    height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
            </div>
          </div>
          
  
          <!--  note list-->
          <notes :notes="notesFilter"   :grid="grid"
          
          
          />
          

        </div>
      </section>
    </div>
    
  </div>
</template>

<script>
import message from '@/components/Message.vue'
import newNote from '@/components/NewNote.vue'
import notes from '@/components/Notes.vue'
import search from '@/components/Search.vue'
export default {
    components: {
        message, notes, newNote, search
    },
    data () {
        return {
            title: 'Notes app',
            search: '',
            message: null,
            grid: true,
            note: {
                title: '',
                descr: '',
                priority: 'light'
            },
            notes: [
                {
                    title: 'First Note',
                    descr: 'Description for First Note',
                    date: new Date(Date.now()).toLocaleString(),
                    priority: 'light',
                    id: 11
                },
                {
                    title: 'Second Note',
                    descr: 'Description for Second Note',
                    date: new Date(Date.now()).toLocaleString(),
                    priority: 'middle',
                    id: 22
                },
                {
                    title: 'Third Note',
                    descr: 'Description for Third Note',
                    date: new Date(Date.now()).toLocaleString(),
                    priority: 'high',
                    id: 33
                }
            ],
            
        }
    },
    computed: {
        notesFilter () {
            let array = this.notes,
                search = this.search
            if (!search) return array
            //Small
            search = search.trim().toLowerCase()
            // Filter
            array = array.filter(function (item) {
              if (item.title.toLowerCase().indexOf(search) !== -1) {
                  return item
              }
            });
            // Error
            return array
        }
    },
    methods: {
        addNote () {
            let {title, descr, priority } = this.note
            if(title === '') {
                this.message = "Title can't me blank!";
                return false
            }
            this.notes.push({
                title,
                descr,
                priority,
                id: this.maxId,
                date: new Date(Date.now()).toLocaleString()
            })
            this.note.title = ''
            this.note.descr = ''
            this.note.priority = 'light'

            this.message = null;
        },
        maxId() {
            let el = this.notes.map(v => v.id)
            let max = Math.max.apply(null, el)
            let newID = max +1
            console.log(newID)
        }
    }
}

</script>

<style>

</style>
