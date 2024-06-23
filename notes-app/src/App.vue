<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <message :message="message" />
          <new-note @create="addedNote" :note="note" />
          <div class="note-header">
            <h1>{{ title }}</h1>
            <search @search="search = $event" :value="search" placeholder="Find your note" />
            <div class="icos">
              <svg :class="{ active: grid }" @click="grid = true" style="cursor: pointer;"
                xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <rect x="3" y="3" width="7" height="7"></rect>
                <rect x="14" y="3" width="7" height="7"></rect>
                <rect x="14" y="14" width="7" height="7"></rect>
                <rect x="3" y="14" width="7" height="7"></rect>
              </svg>
              <svg :class="{ active: !grid }" @click="grid = false" style="cursor: pointer;"
                xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
                stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <line x1="8" y1="6" x2="21" y2="6"></line>
                <line x1="8" y1="12" x2="21" y2="12"></line>
                <line x1="8" y1="18" x2="21" y2="18"></line>
                <line x1="3" y1="6" x2="3" y2="6"></line>
                <line x1="3" y1="12" x2="3" y2="12"></line>
                <line x1="3" y1="18" x2="3" y2="18"></line>
              </svg>
              <title>Two-column</title>
              <desc>Created with Sketch.</desc>
              <defs></defs>
              <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage">
                <g id="Two-column" sketch:type="MSLayerGroup" transform="translate(1.000000, 1.000000)" stroke="#6B6C6E"
                  stroke-width="2">
                  <path
                    d="M26,60 C26,61.1 25.1,62 24,62 L2,62 C0.9,62 0,61.1 0,60 L0,2 C0,0.9 0.9,0 2,0 L24,0 C25.1,0 26,0.9 26,2 L26,60 L26,60 Z"
                    id="Shape" sketch:type="MSShapeGroup"></path>
                  <path
                    d="M62,60 C62,61.1 61.1,62 60,62 L38,62 C36.9,62 36,61.1 36,60 L36,2 C36,0.9 36.9,0 38,0 L60,0 C61.1,0 62,0.9 62,2 L62,60 L62,60 Z"
                    id="Shape" sketch:type="MSShapeGroup"></path>
                </g>
              </g>
              </svg>
            </div>
          </div>
          <notes :grid="grid" @delete="deleteNote" :notes="notesFilter" />
        </div>
      </section>
    </div>
  </div>

</template>

<script>
import Message from '@/components/Message.vue'
import NewNote from '@/components/NewNote.vue'
import Notes from '@/components/Notes.vue'
import Search from '@/components/Search.vue'

export default {
  components: { Message, NewNote, Notes, Search },
  data() {
    return {
      title: 'Notes App',
      search: '',
      message: null,
      grid: true,
      note: {
        title: '',
        description: '',
        priority: 'standart',
        option: ['standart', 'important', 'very-important']
      },
      notes: [
        {
          title: 'First Note',
          description: 'Description for first note',
          date: new Date(Date.now()).toLocaleString(),
          priority: 'standart'
        },
        {
          title: 'Second Note',
          description: 'Description for second note',
          date: new Date(Date.now()).toLocaleString(),
          priority: 'important'
        },
        {
          title: 'Third Note',
          description: 'Description for third note',
          date: new Date(Date.now()).toLocaleString(),
          priority: 'very-important'

        }
      ]
    }
  },
  computed: {
    notesFilter() {
      let array = this.notes,
        search = this.search;
      if (!search) return array
      search = search.trim().toLowerCase()
      array = array.filter(function (item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item
        }
      })
      return array
    }
  },
  methods: {
    addedNote() {
      let { title, description, priority } = this.note

      if (this.notes.length >= 20) return this.message = 'You cannot add more than 50 notes!'

      if (title === '' || description === '') {
        return this.message = 'Title can\'t be blank!'
      } else {
        this.notes.push({
          title,
          description,
          date: new Date(Date.now()).toLocaleString(),
          priority
        });
        this.message = null
        this.note.title = '';
        this.note.description = '';
        this.note.priority = 'standart'

      }



    },
    deleteNote(index) {
      this.notes.splice(index, 1);
    }
  }
}

</script>
