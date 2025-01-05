<!-- 首页标题栏 -->
<template>
  <div class="nav-bar-box">
    <logo-com
      :icon-color="iconColor ? iconColor : '#fff'"
      :font-color="fontColor ? fontColor : '#fff'"
    ></logo-com>
    <div v-config:open_homne_menu class="center">
      <el-menu
        :default-active="route.path"
        class="el-menu-demo"
        mode="horizontal"
        :ellipsis="false"
        router
        :popper-offset="10"
      >
        <template v-for="(item, index) in indexMenuList" :key="index">
          <!-- 只显示启用中的 -->
          <index-menu-item v-if="item.status === 1" :item="item" :key-index="item.name + index" />
        </template>
      </el-menu>
    </div>
    <!-- 用户区域 -->
    <div class="right">
      <!-- 登录注册以及用户展示区域 -->
      <div class="user-box">
        <!-- <div v-if="!appStore.useUserInfoStore.userInfo" class="logon-register-box">
          <el-button v-config:open_sign class="register-btn" @click="openRegisterDialog"
            >注册</el-button
          >
          <el-button class="login-btn" type="primary" @click="openLoginDialog">登录</el-button>
        </div> -->
        <div v-if="appStore.useUserInfoStore.userInfo" class="user-avatar-box">
          <el-dropdown v-config:open_person_in :teleported="false">
            <span class="el-dropdown-link">
              <el-avatar
                v-if="appStore.useUserInfoStore.userInfo.photos.profilePic.url"
                :size="45"
                :src="appStore.useUserInfoStore.userInfo.photos.profilePic.url"
              />
              <el-avatar v-else :size="45">
                {{ appStore.useUserInfoStore.userInfo.name.split('')[0] }}
              </el-avatar>
            </span>
            <template #dropdown>
              <el-dropdown-menu>
                <el-dropdown-item @click="toPerson">个人中心</el-dropdown-item>
                <!-- 管理员入口 -->
                <el-dropdown-item
                  v-if="
                    appStore.useUserInfoStore.userInfo &&
                    appStore.useUserInfoStore.userInfo.roles.indexOf('Admin') !== -1
                  "
                  @click="toAdmin"
                >
                  管理端
                </el-dropdown-item>
                <el-dropdown-item @click="loginout">退出登录</el-dropdown-item>
              </el-dropdown-menu>
            </template>
          </el-dropdown>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
  import appStore from '@/store';
  import LoginDialog from '@/components/LoginDialog/LoginDialog';
  import { storeToRefs } from 'pinia';
  import IndexMenuItem from './components/IndexMenuItem.vue';

  interface IBgcColor {
    bgColor?: string;
    fontColor?: string;
    position?: string;
    iconColor?: string;
  }
  const route = useRoute();
  const props = withDefaults(defineProps<IBgcColor>(), {
    bgColor: '',
    fontColor: '',
    iconColor: '#fff',
    position: 'fixed'
  });

  // 查询首页导航菜单
  const { getIndexMenuList } = appStore.useIndexMenuStore;
  getIndexMenuList();

  // 菜单列表
  const { indexMenuList } = storeToRefs(appStore.useIndexMenuStore);

  const nameColor = computed(() => {
    return props.fontColor ? '#2ddd9d' : 'green';
  });

  // 打开注册弹窗
  const openRegisterDialog = () => {
    LoginDialog(false);
  };

  // 打开登录弹窗
  const openLoginDialog = () => {
    LoginDialog(true);
  };

  const router = useRouter();

  // 跳转至个人中心页
  const toPerson = () => {
    router.push('/person');
  };

  // 跳转至管理员界面
  const toAdmin = () => {
    router.push('/admin');
  };

  // 退出登录
  const { saveToken } = appStore.useTokenStore;
  const { saveUserInfo } = appStore.useUserInfoStore;
  const { setUuid } = appStore.useRefreshStore;
  const loginout = () => {
    saveToken(''); // 清除token
    saveUserInfo(''); // 清除用户信息
    setUuid(); // 全局刷新
    router.push('/');
  };
</script>
<style lang="scss" scoped>
  .nav-bar-box {
    display: flex;
    height: 65px;
    width: 100%;
    box-sizing: border-box;
    align-items: center;
    justify-content: space-between;
    backdrop-filter: blur(8px);
    background-color: v-bind('props.bgColor');
    z-index: 10;
    user-select: none;
    padding: 0 30px;
    position: v-bind('props.position');
    top: 0;
    transition: all 0.3s;
    .center {
      flex: 1;
      height: 100%;
      display: flex;
      justify-content: flex-start;
      align-items: center;
      padding-left: 30px;
      .el-menu {
        border: none;
        height: 100%;
        background-color: rgba(255, 255, 255, 0);
        display: flex;
        justify-content: center;
        align-items: center;
        .el-menu-item {
          height: 100%;
          display: flex;
          justify-content: center;
          align-items: center;
          width: 100%;
          color: v-bind('props.fontColor');
          padding: 0 15px !important;
          letter-spacing: 3px;
          font-size: 16px;
          border-bottom: 4px solid transparent;
          transition: all 0.3s;
          &:hover {
            border-color: #2ddd9d;
            background-color: rgba(#ccc, 0.1);
          }
        }
        .el-sub-menu {
          height: 100%;
          color: v-bind('props.fontColor');
          border-bottom: 4px solid transparent;
          width: 136px;
          &:hover {
            border-bottom: 4px solid #2ddd9d !important;
            background-color: rgba(#ccc, 0.1);
          }
          :deep(.el-sub-menu__title) {
            letter-spacing: 3px;
            font-size: 16px;
            color: v-bind('props.fontColor');
            border: none;
            &:hover {
              background-color: rgba(#ccc, 0.1);
            }
          }
        }
        .is-active {
          background-color: rgba(255, 255, 255, 0);
          border-bottom: 4px solid #2ddd9d !important;
        }
      }
    }
    .right {
      display: flex;
      align-items: center;
      .user-box {
        display: flex;
        .logon-register-box {
          display: flex;
          .el-button {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 30px;
            width: 65px;
          }
          .register-btn {
            margin-left: 15px;
          }
        }
        .user-avatar-box {
          display: flex;
          align-items: center;
          justify-content: center;
          margin-left: 15px;
          cursor: pointer;
          position: relative;
          right: -7px;
          bottom: -5px;
          z-index: 1;
          .name-content {
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            color: v-bind('nameColor');
            background-color: v-bind('iconColor');
          }
        }
      }
    }
  }
</style>
<style lang="scss">
  .navbar-popper-box {
    border: none;
    border-radius: 0;

    .el-menu {
      padding: 0;
      min-width: 134px;
      .el-menu-item {
        height: 50px;
        font-size: 14px;
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        letter-spacing: 2px;
      }
      .el-sub-menu {
        height: 50px;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        color: v-bind('props.fontColor');
        padding: 0 15px !important;
        letter-spacing: 3px;
        font-size: 16px;
        border-bottom: 4px solid transparent;
        transition: all 0.3s;
        &:hover {
          background-color: rgba(#ccc, 0.1);
        }
        :deep(.el-sub-menu__title) {
          letter-spacing: 3px;
          font-size: 16px;
          color: v-bind('props.fontColor');
          border: none;
          &:hover {
            background-color: rgba(#ccc, 0.1);
          }
        }
      }
    }
  }
</style>
