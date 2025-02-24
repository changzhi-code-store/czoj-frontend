<template>
  <div id="global-header">
    <a-row align="center">
      <a-col :span="20">
        <div>
          <a-menu
            mode="horizontal"
            :selected-keys="selectedKeys"
            @menu-item-click="doMenuClick"
          >
            <a-menu-item
              key="0"
              :style="{ padding: 0, marginRight: '38px' }"
              disabled
            >
              <div class="title-bar">
                <div class="title">cz-OJ</div>
              </div>
            </a-menu-item>
            <a-menu-item v-for="item in visibleRoutes" :key="item.path">
              {{ item.name }}
            </a-menu-item>
          </a-menu>
        </div>
      </a-col>
      <a-col :span="4">
        <div>{{ store.state.user?.loginUser?.userName ?? "未登录" }}</div>
      </a-col>
    </a-row>
  </div>
</template>

<style>
#global-header {
  font-weight: bold;
}

.title {
  color: #000;
  font-size: 16px;
}
</style>
<script setup lang="ts">
import { routes } from "../router/routes";
import { useRouter } from "vue-router";
import { computed, ref } from "vue";
import { useStore } from "vuex";
import checkAccess from "@/assets/checkAccess";
import ACCESS_ENUM from "@/assets/accessEnum";

const router = useRouter();
const store = useStore();
const loginUser = store.state.user.loginUser;

// 展示在菜单的路由数量
const visibleRoutes = computed(() => {
  return routes.filter((item, index) => {
    if (item.meta?.hideInMenu) {
      return false;
    }
    if (!checkAccess(store.state.user.loginUser, item.meta?.access as string)) {
      return false;
    }
    return true;
  });
});

setTimeout(() => {
  store.dispatch("user/getLoginUser", {
    userName: "长志管理员",
    userRole: ACCESS_ENUM.ADMIN,
  });
}, 3000);

// 默认主页
const selectedKeys = ref(["/"]);

// 路由跳转后，更新选中的菜单页
router.afterEach((to, from, failure) => {
  selectedKeys.value = [to.path];
});

const doMenuClick = (key: string) => {
  router.push({ path: key });
};
</script>
