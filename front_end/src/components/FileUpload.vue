<template>
  <div>
    <div class="upload-button-container">
      <el-upload
        ref="upload"
        action="http://localhost:5000/upload"
        :on-success="handleSuccess"
        :on-error="handleError"
        list-type="text"
        :auto-upload="true"
        drag
      >
        <el-button size="large" type="success" @click="submitUpload" class="upload-button">上传文件</el-button>
      </el-upload>
    </div>

    <div class="video-container">
      <div v-for="(videoUrl, index) in uploadedVideos" :key="index" class="video-item">
        <video controls width="500">
          <source :src="videoUrl" type="video/mp4">
          你的浏览器不支持视频播放。
        </video>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      uploadedVideos: []  // 存储视频URL的数组
    };
  },
  methods: {
    handleSuccess(response) {
      // 假设服务器返回一个包含视频URL的数组
      this.uploadedVideos = response.videoUrls;
    },
    handleError() {
      this.$message.error('文件上传失败');
    },
    submitUpload() {
      this.$refs.upload.submit(); // 触发上传操作
    }
  }
};
</script>
<style>
.upload-button-container {
  display: flex;
  justify-content: center; /* 水平居中 */
  margin-top: 30px;
  margin-bottom: 50px; /* 添加一些底部间距 */
}
.video-container {
  display: flex;
  flex-direction: column; /* 垂直堆叠视频 */
  justify-content: center; /* 水平居中 */
  align-items: center; /* 垂直居中 */
  width: 100%; /* 确保容器宽度为100% */
}

.video-item {
  margin: 10px auto;
}

</style>
