<template>
    <div class="modal-overlay" @click="closeBookDetails">
        <div class="modal-content" @click.stop>
            <img :src="book.image" alt="Book cover" class="modal-image">
            <h2>{{ book.title }}</h2>
            <p><strong>PRICE:</strong>{{ book.author }}</p>
            <p>{{ book.description }}</p>
            <button @click="closeBookDetails">Close</button>
        </div>
    </div>
</template>

<script>
    export default{
        props: {
            book: Object,
        },
        methods: {
            closeBookDetails(){
                this.$emit('close-details')
            }
        }
    }
</script>

<style scoped>
    .modal-overlay{
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: rgba(0,0,0,0.7);
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .modal-content{
        background: #fff;
        padding: 20px;
        border-radius: 5px;
        width: 400px;
        color: #0c09d3;
    }
    .modal-image{
        max-width: 100%;
        height: auto;
        margin-bottom: 20px;
    }
    h2{
        font-size: 25px;
    }
</style>