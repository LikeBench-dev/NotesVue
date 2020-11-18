<template>
  <div class="notes">
    <note :note="note" :grid="grid" v-for="note in notes" :key="note.id"
          @remove="removeNote"
    
    />
<!--    <div class="note"-->
<!--         -->
<!--         v-for="(note, index) in notes"-->
<!--         :key="index"-->
<!--         :class="[classObject(note), {full: !grid}]">-->
<!--         -->
<!--      <div class="note-header" :class="{ full: !grid}">-->
<!--&lt;!&ndash;        <p>{{ note.title }}</p>&ndash;&gt;-->
<!--        <input class="inp_text_card"-->
<!--               type="text"-->
<!--               :readonly="readonly"-->
<!--               :value="note.title"-->
<!--               :class="{'readonly': readonly === false}" >-->
<!--        <div class="controls">-->
<!--          <i @click="touchInput(note.id)" class="far fa-edit"></i>-->
<!--          <i @click="removeNote(index)" class="far fa-times-circle"></i>-->
<!--        </div>-->
<!--      </div>-->
<!--      <div class="note-body">-->
<!--        <input class="inp_text_card"-->
<!--               type="text"-->
<!--               :readonly="readonly"-->
<!--               :value="note.descr"-->
<!--               :class="{'readonly': readonly === false}" >-->
<!--        <span>{{ note.date }}</span>-->
<!--      </div>-->
<!--    </div>-->
  </div>
</template>

<script>
import note from '@/components/GenerateNote.vue'
export default {
    components: {
        note
    },
    props: {
        notes: {
            type: Array,
            required: true
        },
        grid: {
            type: Boolean,
            required: true
        }
    },
    methods: {
        removeNote (id) {
            let el = this.notes.map(v => v.id).indexOf(id)
            this.notes.splice(el, 1)
        },
        changeNote (elem) {
            console.log(elem.target)
            if (elem.target !== elem.currentTarget) {
                console.log('click')
                this.notes.readonly = true
            }
        }
    }
}

</script>

<style lang="scss">
.inp_text_card {
  color: #3c35a5;
  font-size: 22px;
  width: auto;
  margin: 0;
  padding: 0;
  border: none;
  border-radius: 0;
  &.readonly {
    border-bottom: 1px solid rgba(128, 128, 128, 0.74);
    padding: 5px;
  }
}
.notes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;
}
.note {
  width: 48%;
  padding: 18px 20px;
  margin-bottom: 20px;
  background-color: #ffffff;
  transition: .3s ease-in-out;
  box-shadow: 0 7px 20px rgba(0, 0 , 0, .05);
  
  &.full {
    width: 100%;
    text-align: center;
    .note-body {
      .inp_text_card {
        text-align: center;
      }
    }
  }
  &:hover {
    transform: translateY(-10px);
  }
  &.light {
    box-shadow: 0 7px 20px rgba(0, 0 , 0, .05);
    &:hover {
      box-shadow: 0 7px 20px rgba(0, 0 , 0, .1);
    }
  }
  &.middle {
    box-shadow: 0 7px 20px rgba(84, 171, 90, .3);
    &:hover {
      box-shadow: 0 7px 20px var(--success-color);
    }
  }
  &.high {
    box-shadow: 0 7px 20px rgba(208, 59, 59, .3);
    &:hover {
      box-shadow: 0 7px 20px var(--danger-color);
    }
  }
}
.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  h1 {
    font-size: 32px;
  }
  .controls {
    display: flex;
    align-items: center;
    i {
      color: #999999;
      font-size: 20px;
      cursor: pointer;
      margin-right: 10px;
      &:hover {
        color: #3c35a5;
      }
      &:last-child {
        margin-right: 0;
      }
      &.fa-save {
        font-size: 22px;
      }
    }
  }
  svg {
    margin-right: 12px;
    color: #999999;
    &.active {
      color: #3c35a5;
    }
    &:last-child {
      margin-right: 0;
    }

  }
  &.full {
    justify-content: center;
    p {
      margin-right: 16px;
      &:last-child {
        margin-right: 0;
      }
    }
  }
}
.note-body {
  display: flex;
  flex-direction: column;
  .inp_text_card{
    margin: 30px 0;
    color: black;
  }
  .note-bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    span {
      font-size: 14px;
      color: #999999;
    }
    .radio {
      /*display: inline-flex;*/
      /**/
      display: none;
      &.edit {
        display: flex!important;
      }
      align-items: center;
      justify-content: center;
      margin: 5px;
      input {
        width: 15px;
        margin: 3px;
        cursor: pointer;
        &:checked +label {
          box-shadow: 0 10px 20px rgba(0, 0 , 0, .05);
          border-radius: 0 0 5px 5px;
          font-weight: 500;
        }
        &:checked +label:nth-of-type(1) {
          box-shadow: 0 10px 20px rgba(0, 0 , 0, .05);
          border-bottom: 5px solid var(--white);
        }
        &:checked +label:nth-of-type(2) {
          border-bottom: 5px solid var(--success-color);
        }
        &:checked +label:nth-of-type(3) {
          /*border-bottom: 2px solid rgba(208, 59, 59, .7);*/
          border-bottom: 5px solid var(--danger-color);
        }
      }
      label {
        margin: 5px 20px 5px 5px;
        cursor: pointer;
        &:last-child {
          margin-right: 0;
        }
      }
    }
  }
  p {
    margin: 20px 0;
  }

}
</style>
