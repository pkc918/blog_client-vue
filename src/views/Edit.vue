<template>
  <div id="edit">
    <h1>编辑文章</h1>
    <h3>文章标题</h3>
    <el-input v-model="title"></el-input>
    <p class="msg">{{ title.length }}/30</p>
    <h3>内容简介</h3>
    <el-input v-model="description" type="textarea" rows="4"></el-input>
    <p class="msg">{{ description.length }}/30</p>
    <h3>文章内容</h3>
    <el-input v-model="content" type="textarea" rows="10"></el-input>
    <p class="msg">{{ content.length }}/200</p>
    <p>
      <label style="margin-right: 5px;">是否展示到首页</label>
      <el-switch
          v-model="atIndex"
          active-color="#13ce66"
      >
      </el-switch>
    </p>
    <el-button @click="onEdit" plain type="primary">确定</el-button>
  </div>
</template>

<script>
import blog from '@/api/blog';

export default {
  name: 'Create',
  data() {
    return {
      blogId: null,
      title: '',
      description: '',
      content: '',
      atIndex: false
    };
  },
  created() {
    this.blogId = this.$route.params.blogId
    blog.getDetail({blogId: this.blogId})
        .then(res => {
          this.title = res.data.title
          this.description = res.data.description
          this.content = res.data.content
          this.atIndex = res.data.atIndex
        })
  },
  methods: {
    onEdit() {
      blog.updateBlog({
        blogId: this.blogId
      }, {
        title: this.title,
        content: this.content,
        description: this.description,
        atIndex: this.atIndex
      })
          .then(res => {
            this.$message.success(res.msg)
            this.$router.push({path: `/detail/${res.data.id}`})
          })
    }
  }
};
</script>

<style lang="scss" scoped>
#edit, #create {
  padding: 30px;

  h1 {
    text-align: center;
  }

  .msg {
    text-align: right;
    font-size: 12px;
    color: red;
  }

  ::v-deep .el-input__inner, ::v-deep .el-textarea__inner {
    border: 1px solid #42b983;
    background: #ddd;
  }
}
</style>
