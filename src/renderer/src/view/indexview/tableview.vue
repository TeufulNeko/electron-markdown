<template>
  <el-table :data="localdata">
    <el-table-column type="index" label="id" width="50px" />
    <el-table-column prop="id" label="SQL-ID" width="150px" />
    <el-table-column prop="name" label="Title" />
    <el-table-column prop="createdate" label="CreateDate" />
    <el-table-column prop="update" label="UpDate" />
    <el-table-column prop="setting" label="satting">
      <template #default="scope">
        <el-button class="edit" type="primary" @click="editfile(scope)">Edit</el-button>
        <el-button class="del" type="danger" @click="delfilebydb(scope)">Del</el-button>
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
export default {
  name: 'Tableview',
  // eslint-disable-next-line vue/require-prop-types
  props: ['paramdata'],
  data() {
    return {
      localdata:[]
    }
  },
  mounted(){
    this.localdata=this.paramdata
  },
  methods: {
    editfile(scope) {
      // eslint-disable-next-line no-undef
      this.$router.push({ name: 'edit', query: { value: scope.row.id }, replace: true })
    },
    async delfilebydb(scope) {
      console.log('scope.row.id: ' + scope.row.id)
      await window.dbcontrol.deletefilebydb(scope.row.id)
      this.localdata.splice(scope.$index)
    }
  }
}
</script>

<style>
@media (prefers-color-scheme: dark) {
  .el-table {
    --el-table-text-color: #86a5b1;
    --el-table-header-text-color: #86a5b1;
    --el-table-row-hover-bg-color: #2f3241;
    --el-table-current-row-bg-color: #2f3241;
    --el-table-header-bg-color: #2f3241;
    --el-table-bg-color: #2f3241;
    --el-table-tr-bg-color: #2f3241;
    --el-table-expanded-cell-bg-color: #2f3241;
    --el-table-fixed-left-column: inset 10px 0 10px -10px rgba(0, 0, 0, 0.15);
    --el-table-fixed-right-column: inset -10px 0 10px -10px rgba(0, 0, 0, 0.15);
    --el-bg-color: #2f3241;
  }
}
</style>