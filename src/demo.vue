<template>
  <div style="background: #ececec; padding: 30px">
    <a-card>
      <a-table
        :columns="columns"
        :data-source="data"
        bordered
        :customRow="customRow"
      >
        <template #bodyCell="{ column, record, text }">
          <template
            v-if="column.dataIndex === 'name' && record.canEdit === true"
          >
            <a-input :size="small" v-model:value="record.name"></a-input>
          </template>
          <template
            v-if="column.dataIndex === 'address' && record.canEdit === true"
          >
            <a-select
              v-model:value="record.address"
              style="width: 100%"
              placeholder="Tags Mode"
              :options="options"
              @change="handleChange"
            ></a-select>
          </template>
          <template v-else>
            {{ text }}
          </template>
        </template>
        <template #title></template>
        <template #footer>Footer</template>
      </a-table>
    </a-card>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

const columns = [
  {
    title: "商品名称",
    dataIndex: "name",
    ellipsis: true,
  },
  {
    title: "Cash Assets",
    dataIndex: "money",
    ellipsis: true,
  },
  {
    title: "Address",
    dataIndex: "address",
    ellipsis: true,
  },
  {
    title: "Address1",
    dataIndex: "address1",
    ellipsis: true,
  },
  {
    title: "Address2",
    dataIndex: "address2",
    ellipsis: true,
  },
  {
    title: "Address3",
    dataIndex: "address3",
    ellipsis: true,
  },
];

const data = [
  {
    key: "1",
    name: "John Brown",
    money: "￥300,000.00",
    address: "a",
    address1: "New York No. 1 Lake Park",
    address2: "New York No. 1 Lake Park",
    address3: "New York No. 1 Lake Park",
    canEdit: false,
  },
  {
    key: "2",
    name: "Jim Green",
    money: "￥1,256,000.00",
    address: "b",
    address1: "New York No. 1 Lake Park",
    address2: "New York No. 1 Lake Park",
    address3: "New York No. 1 Lake Park",
    canEdit: false,
  },
  {
    key: "3",
    name: "Joe Black",
    money: "￥120,000.00",
    address: "c",
    address1: "New York No. 1 Lake Park",
    address2: "New York No. 1 Lake Park",
    address3: "New York No. 1 Lake Park",
    canEdit: false,
  },
];

export default defineComponent({
  setup() {
    const handleChange = (value) => {
      console.log(data);
    };
    const customRow = (record, index) => {
      return {
        onClick: (event) => {
            data[index].canEdit = true
        },
      };
    };
    return {
      data,
      columns,
      handleChange,
      customRow,
      options: [
        { value: "a", title: "test1" },
        { value: "b", title: "test2" },
        { value: "c", title: "test3" },
      ],
    };
  },
});
</script>
<style>
th.column-money,
td.column-money {
  text-align: right !important;
}
</style>
