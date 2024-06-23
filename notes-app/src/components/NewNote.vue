<template>
    <div class="new-note">
        <label>Title</label>
        <input v-model="note.title" type="text" />
        <div class="choose-priority">
            <select v-model="note.priority">
                <option 
                v-for="(option, index) in note.option" 
                :key="index" 
                :value="option"
                >
                    {{ option }}
                </option>
            </select>
        </div>
        <label>Description</label>
        <textarea v-model="note.description"></textarea>
        <button class="btn btnPrimary" @click="addedNote">Create new note</button>
    </div>
</template>

<script>
export default {
    props: {
        note: {
            type: Object,
            required: true
        }
    },
    methods: {
        addedNote() {
            this.$emit('create', this.note)
        }
    }
}
</script>

<style lang="scss">
.new-note {
    text-align: center;

    .choose-priority {
        display: flex;
        justify-content: flex-start;

        select{
            padding: 5px 10px 5px 10px;
            border-radius: 4px;
            font-family: Arial, Helvetica, sans-serif;
        }
    }
}

.btn {
    margin-top: 20px;
    margin-bottom: 20px;
}
</style>