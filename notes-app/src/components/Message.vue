<template>
        <div class="message" v-if="message">
            <p style=" font-size: 20px; text-transform: uppercase; font-family: sans-serif;">{{ message }}
            </p>
          </div>
</template>

<script>
export default {
    props: {
        message: {
            type: String,
            required: true,
            default: 'message default'
        }
    }
}
</script>

<style lang="scss" scoped>
.message {
    text-align: center;
    margin-bottom: 10px;
}
p {
    color: red;

}
</style>