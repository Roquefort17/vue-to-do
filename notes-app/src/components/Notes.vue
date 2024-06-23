<template>
    <div class="notes">
        <div :class="['note', note.priority, { full: !grid }]" class="note" v-for="(note, index) in notes" :key="index">
            <div :class="{ full: !grid }" class="note-header">
                <p>{{ note.title }}</p>
                <p style="cursor: pointer;" @click="deleteNote(index)">x</p>
            </div>
            <div class="note-body">
                <p>{{ note.description }}</p>
                <span>{{ note.date }}</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
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
        deleteNote(index) {
            this.$emit('delete', index)
            console.log(`Note id ${index} - removed`)
        }
    }
}
</script>

<style lang="scss">
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
    background-color: #fff;
    border-radius: 3px;
    transition: all 0.25s cubic-bezier(.02, .01, .47, 1);

    &.simple {
        border-left: 5px solid #31df1e;
    }

    &.important {
        border-left: 5px solid #f39c12;
    }

    &.very-important {
        border-left: 5px solid #e74c3c;
    }

    &:hover {
        box-shadow: 0 30px 30px rgba(0, 0, 0, 0.04);
        transform: translate(0, -6px);
        transition-delay: 0s !important;
    }


    &.full {
        width: 100%;
        text-align: center;
    }

}

.note-header {
    display: flex;
    align-items: center;
    justify-content: space-between;


    p {

        font-size: 22px;
        color: #5314c8;

    }

    h1 {
        font-size: 30px
    }

    svg {
        margin-right: 12px;
        color: #999;
        cursor: pointer;

        &.active {
            color: #402caf
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
    p {
        margin: 20px 0;
    }

    span {
        font-size: 14px;
        color: #999
    }

}
</style>