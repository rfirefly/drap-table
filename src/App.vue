<template>
  <div id="app">
    <drap-table :columns="columns" :data-source="data">
      <a-table  slot="expandedRowRender" :columns="innerColumns" :data-source="innerData" rowKey="name" :pagination="false">
      </a-table>
    </drap-table>
    <a-button @click="showSomething">look</a-button>

    <!-- <Test></Test> -->
  </div>
</template>

<script>
import DrapTable from "./components/DrapTable";
// import Test from "./components/Test.vue"
const columns = [
  {
    title: "Name",
    dataIndex: "name",
    key: "name",
    scopedSlots: { customRender: "name" },
  },
  {
    title: "Age",
    dataIndex: "age",
    key: "age",
    width: 80,
  },
  {
    title: "Address",
    dataIndex: "address",
    key: "address 1",
    ellipsis: true,
  },
  {
    title: "Long Column  Long Column",
    dataIndex: "address",
    key: "address 2",
    ellipsis: true,
  },
  {
    title: "Long Column Long Column",
    dataIndex: "address",
    key: "address 3",
    ellipsis: true,
  },
  {
    title: "Long Column",
    dataIndex: "address",
    key: "address 4",
    ellipsis: true,
  },
];

const data = [
  {
    key: "1",
    name: "John Brown",
    age: 0,
    address: "New York No. 1 Lake Park",
    tags: ["nice", "developer"],
  },
  {
    key: "2",
    name: "Jim Green",
    age: 1,
    address: "London No. 2 Lake Park",
    tags: ["loser"],
  },
  {
    key: "3",
    name: "Joe Black",
    age: 2,
    address: " Sidney No. 1 Lake Park",
    tags: ["cool", "teacher"],
  },
  {
    key: "4",
    name: "Jim Green",
    age: 3,
    address: "London No. 2 Lake Park, London No. 2 Lake Park",
    tags: ["loser"],
  },
  {
    key: "5",
    name: "Joe Black",
    age: 4,
    address: "Sidney No. 1 Lake Park, Sidney No. 1 Lake Park",
    tags: ["cool", "teacher"],
  },
];

const innerColumns = [
  {
    title: "kaa",
    dataIndex: "name",
    key: "name",
    scopedSlots: { customRender: "name" },
  },
  {
    title: "kvb",
    dataIndex: "age",
    key: "age",
    width: 80,
  },
];

const innerData = [
  {
    name: "aa",
    age: 20,
  },
  {
    name: "bb",
    age: 21,
  },
];

export default {
  name: "App",
  components: {
    DrapTable,
    // Test
  },
  data() {
    return {
      data,
      columns,
      innerColumns,
      innerData,
    };
  },
  mounted() {
  },
  methods: {
    handleClick() {
      this.data.push({
        key: this.data.length + 1,
        name: "Jim Green",
        age: 5,
        address: "London No. 2 Lake Park, London No. 2 Lake Park",
        tags: ["loser"],
      });
    },
    expandedRowRender() {
      let createElement = this.$createElement;
      return createElement(
        "a-table",
        {
          attrs: {
            columns: this.innerColumns,
            dataSource: this.innerData,
            pagination: false,
          },
        },
        ["5555"]
        // this.$slots.default
      );
    },
    showSomething() {
      
      console.log('this.expandedRow: ', this.expandedRow);
    },
  },
};
</script>

<style>
</style>
