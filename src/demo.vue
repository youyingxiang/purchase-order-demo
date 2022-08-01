
<template>
  <div>
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
            <a-input v-model:value="record.name"></a-input>
          </template>
          <template
            v-else-if="column.dataIndex === 'code' && record.canEdit === true"
          >
            <a-select
              style="width: 100%"
              v-model:value="record.code"
              show-search
              placeholder="input here"
              :filter-option="false"
              :not-found-content="null"
              :dropdownMatchSelectWidth="400"
              :options="autoCompletData.data"
              @search="handleSearch"
              @select="handleSelect"
            >
              <template #suffixIcon>
                <DashOutlined @click="handleClick" />
              </template>

              <template #option="row">
                <a-row justify="center"  align="middle">
                  <a-col
                    :span="8"
                    style="
                      border-bottom: 1px solid #f0f0f0;
                      transition: background 0.3s;
                    "
                    >{{ row.name }}</a-col
                  >
                  <a-col
                    :span="8"
                    style="
                      border-bottom: 1px solid #f0f0f0;
                      transition: background 0.3s;
                    "
                    >{{ row.code }}</a-col
                  >
                  <a-col
                    :span="8"
                    style="
                      border-bottom: 1px solid #f0f0f0;
                      transition: background 0.3s;
                    "
                    >{{ row.money }}</a-col
                  >
                </a-row>
              </template>

              <template #dropdownRender="{ menuNode: menu }">
                <a-row
                  justify="center"
                  style="padding: 5px 12px; border-bottom: 1px solid #f0f0f0;background:#f0f0f0"
                >
                  <a-col
                    :span="8"
                    v-for="(row, index) in autoCompletData.columns"
                    :key="index"
                    >{{ row.title }}</a-col
                  >
                </a-row>
                <v-nodes :vnodes="menu"/>
                <a-row justify="center" style="padding: 5px 12px">
                  <a-col :span="8"></a-col>
                  <a-col :span="8">
                    <plus-outlined />
                    Add item
                  </a-col>
                  <a-col :span="8"></a-col>
                </a-row>
              </template>
            </a-select>
          </template>
          <template
            v-else-if="
              column.dataIndex === 'address' && record.canEdit === true
            "
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

<script>
import _ from "lodash";
import { DashOutlined } from "@ant-design/icons-vue";

const columns = [
  {
    title: "商品名称",
    dataIndex: "name",
    ellipsis: true,
  },
  {
    title: "条形码",
    dataIndex: "code",
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
    name: "John Brown",
    code: "121212",
    money: "￥300,000.00",
    address: "a",
    address1: "New York No. 1 Lake Park",
    address2: "New York No. 1 Lake Park",
    address3: "New York No. 1 Lake Park",
    canEdit: false,
  },
  {
    name: "Jim Green",
    code: "331121212",
    money: "￥1,256,000.00",
    address: "b",
    address1: "New York No. 1 Lake Park",
    address2: "New York No. 1 Lake Park",
    address3: "New York No. 1 Lake Park",
    canEdit: false,
  },
  {
    name: "Joe Black",
    code: "44121212",
    money: "￥120,000.00",
    address: "c",
    address1: "New York No. 1 Lake Park",
    address2: "New York No. 1 Lake Park",
    address3: "New York No. 1 Lake Park",
    canEdit: false,
  },
];

export default {
  components: {
    DashOutlined,
    VNodes: (_, { attrs }) => {
      return attrs.vnodes;
    },
  },
  data() {
    return {
      data,
      columns,
      value: "",
      autoCompletData: {},
      options: [
        { value: "a", title: "test1" },
        { value: "b", title: "test2" },
        { value: "c", title: "test3" },
      ],
    };
  },
  methods: {
    customRow(record, index) {
      return {
        onClick: (event) => {
          this.data[index].canEdit = true;
          // this.value = record.code;
          _(this.data).forEach((v, k) => {
            if (k !== index) {
              v.canEdit = false;
            }
            return v;
          });
        },
      };
    },
    selectTableCustomRow(record, index) {
      return {
        onClick: (event) => {
          console.log(record);
        },
      };
    },
    handleChange(value) {},
    handleClick() {
      alert("123");
    },
    handleSelect(value, option) {
      console.log(option);
    },
    handleSearch(value) {
      this.autoCompletData = {
        columns: [
          {
            title: "商品名称",
            dataIndex: "name",
            ellipsis: true,
          },
          {
            title: "条形码",
            dataIndex: "code",
            ellipsis: true,
          },
          {
            title: "Cash Assets",
            dataIndex: "money",
            ellipsis: true,
          },
        ],
        data: [
          {
            id: 1,
            value: 1,
            name: "Joe Black",
            code: "44121212",
            money: "￥120,000.00",
          },
          {
            id: 2,
            value: 2,
            name: "Joe Black",
            code: "44121212",
            money: "￥120,000.00",
          },
          {
            id: 3,
            value: 3,
            name: "Joe Black",
            code: "44121212",
            money: "￥120,000.00",
          },
        ],
      };
    },
  },
};
</script>
<style>
th.column-money,
td.column-money {
  text-align: right !important;
}
.search-dropdown-table .ant-select-item {
  padding: 0px !important;
}
.ant-table-row > .select-table-td {
  border-right: 1px solid #5e5c5c;
  border-bottom: 1px solid;
  transition: background 0.3s;
  position: relative;
  padding: 16px 16px;
  overflow-wrap: break-word;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  word-break: keep-all;
}
</style>
