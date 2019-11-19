<template>
  <div class="user-wrapper">
    <div class="content-box">
	 <a-dropdown :trigger="['click']">
	     <a class="ant-dropdown-link" href="#"> 
			 <span class="action">
				<a-icon type="desktop"/> 北京中心-产品拓展部 <a-icon type="down" /> 
			 </span>
		 </a>
	     <a-menu slot="overlay">
			<a-sub-menu title="北京中心" key="北京" >
				<a-menu-item><a-icon type="desktop"/>行业售后部</a-menu-item>
				<a-menu-item><a-icon type="desktop"/>开发1部</a-menu-item>
			</a-sub-menu>
			<a-sub-menu title="天津中心" key="天津" icon="desktop">
				<a-menu-item><a-icon type="desktop"/>渠道售后部</a-menu-item>
				<a-menu-item><a-icon type="desktop"/>产品研发部</a-menu-item>
			</a-sub-menu>
			<a-sub-menu title="第三中心" disabled>
				<a-menu-item><a-icon type="desktop"/>备用1</a-menu-item>
				<a-menu-item><a-icon type="desktop"/>备用2</a-menu-item>
			</a-sub-menu>
	     </a-menu>
	   </a-dropdown>
      <a href="../../assets/help.pdf" target="_blank">
        <span class="action">
          <a-icon type="question-circle-o"></a-icon>
        </span>
      </a>
      <!-- <notice-icon class="action"/> -->
      <a-dropdown>
        <span class="action ant-dropdown-link user-dropdown-menu">
          <a-icon type="user" />
          <span>  {{ nickname() }}</span>
        </span>
        <a-menu slot="overlay" class="user-dropdown-menu-wrapper">
          <!-- <a-menu-item key="0">
            <router-link :to="{ name: 'center' }">
              <a-icon type="user"/>
              <span>个人中心</span>
            </router-link>
          </a-menu-item>
          <a-menu-item key="1">
            <router-link :to="{ name: 'settings' }">
              <a-icon type="setting"/>
              <span>账户设置</span>
            </router-link>
          </a-menu-item>
          <a-menu-divider/> -->
          <a-menu-item key="3">
            <a href="javascript:;" @click="handleLogout">
              <a-icon type="logout"/>
              <span>退出登录</span>
            </a>
          </a-menu-item>
        </a-menu>
      </a-dropdown>
      <a-dropdown>
          <span class="action ant-dropdown-link user-dropdown-menu">
            <a-icon type="setting" />
          </span>
          <a-menu slot="overlay" class="user-dropdown-menu-wrapper">
              <a-menu-item key="0">
                <a href="javascript:;">
                  <a-icon type="reload"/>
                  <span>重启系统</span>
                </a>
            </a-menu-item>
              <a-menu-item key="1">
                <a href="javascript:;">
                  <a-icon type="poweroff"/>
                  <span>关闭系统</span>
                </a>
            </a-menu-item>
          </a-menu>
        </a-dropdown>
    </div>
  </div>
</template>

<script>
import NoticeIcon from '@/components/NoticeIcon'
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'UserMenu',
  components: {
    NoticeIcon
  },
  methods: {
    ...mapActions(['Logout']),
    ...mapGetters(['nickname', 'avatar']),
    handleLogout () {
      const that = this

      this.$confirm({
        title: '提示',
        content: '真的要注销登录吗 ?',
        onOk () {
          return that.Logout({}).then(() => {
            window.location.reload()
          }).catch(err => {
            that.$message.error({
              title: '错误',
              description: err.message
            })
          })
        },
        onCancel () {
        }
      })
    }
  }
}
</script>
