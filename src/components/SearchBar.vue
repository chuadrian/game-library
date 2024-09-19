<template>
    <div>
        <input v-model="searchQuery" type="text" placeholder="Search for a Game" />
    </div>
</template>

<script>
    export default {
        props: {
            modelValue: String,
        },
        computed: {
            searchQuery: {
                get(){
                    return this.modelValue;
                },
                set(value){
                    this.$emit('update:modelValue', value);
                },
            },
        },
    }
</script>
<style scoped>
    .search-container {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
}

input {
    padding: 12px 20px;
    width: 100%;
    max-width: 400px;
    border: 2px solid #00ffcc;
    border-radius: 25px;
    font-size: 16px;
    color: #333;
    background: #f4f4f4;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    transition: all 0.3s ease;
}

input::placeholder {
    color: #888;
}

input:focus {
    border-color: #00c6ff;
    background: #fff;
    outline: none;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}
@media (max-width: 768px) {
  input {
    padding: 10px 15px;
    max-width: 300px;
    font-size: 14px;
  }
}

@media (max-width: 480px) {
  input {
    padding: 8px 12px;
    max-width: 250px;
    font-size: 12px;
  }
}

@media (max-width: 320px) {
  input {
    padding: 6px 10px;
    max-width: 200px;
    font-size: 10px;
  }
}
</style>
