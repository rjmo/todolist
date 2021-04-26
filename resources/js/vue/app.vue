<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">Todo list</h2>
            <addItemForm
                v-on:reloadlist="getList()"
 />
        </div>
        <listView
        :items="items"
        v-on:reloadlist="getList()"
         />
    </div>
</template>

<script>
import addItemForm from "./addItemForm.vue";
import listView from "./listView.vue";
export default {
    components: {
        addItemForm,
        listView
    },
    data: function() {
        return {
            items: []
        };
    },
    methods: {
        getList() {
            axios
                .get("api/item")
                .then(response => {
                    this.items = response.data;
                })
                .catch(error => {
                    console.log(error);
                });
        }
    },
    created() {
        this.getList();
    }
};
</script>

<style scoped>
.todoListContainer {
    width: 350px;
    margin: auto;
}
.heading {
    background: whitesmoke;
    padding: 10px;
}
#title {
    text-align: center;
}
</style>
