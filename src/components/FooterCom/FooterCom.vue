<template>
  <div class="footer-box">
    <!-- 相关信息 -->
    <div class="recommend">
      <!-- 关于我们 -->
      <div class="about-me">
        <h1>关于我们</h1>
        <p>职行AI简历是一款智能简历制作工具</p>
        <p>致力于为求职者提供专业的简历解决方案</p>
        <p>让简历制作更简单、更高效</p>
      </div>
      <!-- 产品服务 -->
      <div class="about-me">
        <h1>产品服务</h1>
        <p>智能简历制作</p>
        <p>在线简历模板</p>
        <p>简历导出服务</p>
      </div>
      <!-- 联系我们 -->
      <div class="links">
        <h1>联系我们</h1>
        <p>商务合作：business@zhixing.ai</p>
        <p>用户反馈：feedback@zhixing.ai</p>
        <p>加入我们：hr@zhixing.ai</p>
      </div>
    </div>
    <!-- 版权声明 -->
    <div class="copyright-notice">
      <p>Copyright © 2024 职行AI简历 All Rights Reserved.</p>
    </div>
    <!-- 备案号 -->
    <div class="icp-record-number">
      <p>
        <a href="https://beian.miit.gov.cn" target="_blank" rel="noopener noreferrer"
          >蜀ICP备xxx号-4</a
        >
      </p>
    </div>
  </div>
</template>
<style lang="scss" scoped>
  .footer-box {
    width: 100%;
    background-color: #333333;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 15px 0;
    .recommend {
      display: flex;
      padding: 20px 0;
      border-bottom: 1px solid #5b5b5b;
      width: 600px;
      height: 250px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      h1 {
        color: #a3a5a7;
        font-size: 16px;
        padding-bottom: 10px;
        letter-spacing: 1px;
        font-weight: 500;
      }
      .about-me {
        height: 100%;
        display: flex;
        flex-direction: column;
        padding-top: 30px;
        p {
          color: #fff;
          display: flex;
          justify-content: flex-start;
          margin-bottom: 10px;
          font-size: 14px;
          a {
            color: inherit;
            text-decoration: none;
            letter-spacing: 2px;
            transition: all 0.3s;
            &:hover {
              color: rgb(123, 238, 123);
            }
          }
        }
      }
      .links {
        display: flex;
        flex-direction: column;
        height: 100%;
        padding-top: 30px;
        p {
          color: #fff;
          display: flex;
          justify-content: flex-start;
          margin-bottom: 10px;
          font-size: 14px;
          a {
            color: inherit;
            text-decoration: none;
            letter-spacing: 2px;
            transition: all 0.3s;
            &:hover {
              color: rgb(123, 238, 123);
            }
          }
        }
      }
    }
    .copyright-notice {
      margin: 15px 0;
      p {
        color: #757c88;
        font-size: 12px;
      }
    }
    .icp-record-number {
      display: flex;
      p {
        color: #757c88;
        font-size: 12px;
        display: flex;
        align-items: center;
        margin: 0 10px;
        a {
          color: inherit;
          text-decoration: none;
          letter-spacing: 2px;
          transition: all 0.3s;
          &:hover {
            color: rgb(123, 238, 123);
          }
        }
      }
    }
  }
</style>
