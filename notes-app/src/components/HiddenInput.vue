<template>
    <div>
        <div v-if="isEditing">
            <input 
            v-model="editedTitle" 
            @keyup.enter="saveEdit" 
            @keyup.esc="cancelEdit" 
            ref="editTitleInput" 
            />
        </div>
        <div v-else @click="startEdit">
            <p>{{ title }}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            isEditing: false,
            editedTitle: this.title
        };
    },
    methods: {
        startEdit() {
            this.isEditing = true;
            this.$nextTick(() => {
                this.$refs.editTitleInput.focus();
            });
        },
        saveEdit() {
            this.isEditing = false;
            this.$emit('save', this.editedTitle);
        },
        cancelEdit() {
            this.isEditing = false;
            this.editedTitle = this.title;
        }
    }
};
</script>

<style scoped>
p {
    cursor: pointer;
    font-size: 20px;
    color: #5314c8;
}
input {
    color: #5314c8;
    width: 100%;
    border: none;
    border: 2px solid #10e33d;
    outline: none;
}
</style>