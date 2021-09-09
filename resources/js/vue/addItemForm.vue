<template>
  <div class="addItem">
    <input type="text" v-model="item.name" />
    <font-awesome-icon
      icon="plus-square"
      @click="addItem()"
      :class="[ item.name ? 'active' : 'inactive', 'plus']"
    />
  </div>
</template>
<script>
export default {
  data() {
    return {
      item: {
        name: ""
      }
    };
  },
  methods: {
    addItem() {
      if (this.item.name == "") {
        return;
      }
      axios
        .post("api/item/store", {
          item: this.item
        })
        .then(response => {
          if (response.status == 201) {
            //   if status success, clear the old data from item name
            this.item.name = "";
            this.$emit("reloadlist");
          }
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>
<style scoped>
.addItem {
  display: flex;
  justify-content: center;
  align-items: center;
}

input {
  background: #f7f7f7;
  border: 0px;
  outline: none;
  padding: 5px;
  margin-right: 5px;
}
.plus {
  font-size: 20px;
}
.active {
  color: #00ce25;
}
.inactive {
  color: #999999;
}
</style>