<template>
  <div class="hello">
    <!-- 这段代码是界面显示 -->
    <div v-for="(attachment, index) in attachmentList" :key="index">
      <el-link
        :key="attachment.path"
        :href="attachment.path"
        style="display: inline-block"
        type="success"
        :underline="false"
      >
        {{ attachment.name }}
      </el-link>
      <el-button
        type="text"
        style="display: inline-block; margin-left: 30px"
        @click="previewFile(attachment)"
      >
        预览</el-button
      >
    </div>

    <!-- 点击上面的预览按钮会弹出文件预览框 -->
    <el-dialog
      :close-on-click-modal="true"
      title="文件预览"
      type="primary"
      v-modal="previewDialog"
      width="80%"
      left
    >
      <iframe :src="attachmentSrc" frameborder="0" width="100%" height="800"></iframe>
    </el-dialog>
    <el-button type="primary" @click="close">关闭</el-button>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  data() {
    return {
      previewDialog: false,
      attachmentSrc: "",
      attachmentList: [
        {
          name: "阿里docx链接",
          path:
            "http://allen2023-06-09.oss-cn-beijing.aliyuncs.com/world.doc?Expires=1688576856&OSSAccessKeyId=TMP.3KdCDaVhtJEFwiwSLsGY64JxdzpJNtvX7eJWFoHkSrE7HHq69GNzzR6DEM6LZuoqFZ6QSFQEs5vR8xXdrx9hkrWdk6GkJD&Signature=erSCKBh%2BLsYu%2BH6mu5T1sDZVhGQ%3D",
        },
        {
          name: "网链pdf文件",
          path:
            "http://storage.xuetangx.com/public_assets/xuetangx/PDF/PlayerAPI_v1.0.6.pdf",
        },
        {
          name: "本地发票文件",
          path: "../assets/顺丰电子发票.pdf",
        },
        {
          name: "",
          path: "https://vfdgfdsgdfsgfg/attachment/example4.xlsx",
        },
        {
          name: "加密ppt文件",
          path: "https://www.kdocs.cn/l/cj3hwGhj4aw5",
        },
      ],
    };
  },

  methods: {
    // 预览文件
    previewFile(attachment) {
      // 根据文件格式显示预览内容
      const fileExtension = attachment.path.split(".").pop().toLowerCase();
      if (fileExtension === "xlsx" || fileExtension === "docx") {
        this.attachmentSrc =
          "https://file.kkview.cn/onlinePreview?url=" + attachment.path;
      } else {
        this.attachmentSrc = attachment.path;
      }
      this.previewDialog = true;
    },
    close() {
      this.previewDialog = false;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
