<template>
  <div class="app-container">
    <el-input 
      v-model="filename" 
      placeholder="请输入文件名称！ (default file)" 
      style="width:300px;"
      prefix-icon="el-icon-document" />

    <el-button 
    :loading="downloadLoading" 
    style="margin-bottom:20px;" 
    type="primary" 
    icon="el-icon-document" 
    @click="handleDownload">

      导出 Zip
    </el-button>

    <el-table 
    v-loading="listLoading" 
    :data="list" 
    element-loading-text="拼命加载中" 
    border 
    fit 
    highlight-current-row>


      <el-table-column 
      align="center" 
      label="ID" 
      width="95">
        <template slot-scope="scope">
          {{ scope.$index }}
        </template>
      </el-table-column>
      <el-table-column label="Title">
        <template slot-scope="scope">
          {{ scope.row.title }}
        </template>
      </el-table-column>
      <el-table-column label="Author" width="95" align="center">
        <template slot-scope="scope">
          <el-tag>{{ scope.row.author }}</el-tag>
        </template>
      </el-table-column>
      <el-table-column label="Readings" width="115" align="center">
        <template slot-scope="scope">
          {{ scope.row.pageviews }}
        </template>
      </el-table-column>
      <el-table-column align="center" label="Date" width="220">
        <template slot-scope="scope">
          <i class="el-icon-time" />
          <span>{{ scope.row.display_time }}</span>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import { fetchList } from '@/api/article'

export default {
  name: 'ExportZip',
  data() {
    return {
      list: null,
      listLoading: true,
      downloadLoading: false,
      filename: ''
    }
  },
  created() {
    //页面初始化调用次方法
    this.fetchData()
  },
  methods: {
    async fetchData() {
      this.listLoading = true//进度条显示
      const { data } = await fetchList()//调接口
      this.list = data.items//拿到返回数据
      this.listLoading = false//关闭进度条
    },

    // 导出zip按钮
    handleDownload() {
      this.downloadLoading = true
      import('@/vendor/Export2Zip').then(zip => {

        //设置参数
        const tHeader = ['Id', 'Title', 'Author', 'Readings', 'Date']
        const filterVal = ['id', 'title', 'author', 'pageviews', 'display_time']
        const list = this.list
        const data = this.formatJson(filterVal, list)
        
        // 调用和zip的方法
        zip.export_txt_to_zip(tHeader, data, this.filename, this.filename)
        this.downloadLoading = false
      })
    },
    formatJson(filterVal, jsonData) {
      return jsonData.map(v => filterVal.map(j => v[j]))
    }
  }
}
</script>
