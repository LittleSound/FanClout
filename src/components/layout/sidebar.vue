<template>
  <div class="sidebar">
    <SearchBox class="sidebar-search-box" />
    <MetaCoinStatus class="sidebar-meta-coin-status" :price="mtbtPrice" />
    <RightBarLogIn class="sidebar-login" v-if="!isLoggedIn" />
    <TopWeeklyCreators class="sidebar-top-weekly-creators" />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import SearchBox from '@/components/SearchBox'
import MetaCoinStatus from '@/components/MetaCoinStatus'
import TopWeeklyCreators from '@/components/TopWeeklyCreators'
import RightBarLogIn from '@/components/RightBarLogIn'
import { getMTBTPrice } from '../../contracts'

export default {
  name: 'Sidebar',
  components: { TopWeeklyCreators, MetaCoinStatus, SearchBox, RightBarLogIn },
  data () {
    return {
      searchValue: '',
      mtbtPrice: 0
    }
  },
  computed: {
    ...mapState(['userInfo']),
    isLoggedIn () {
      return this.userInfo && this.userInfo.id !== -1
    }
  },
  watch: {},
  async mounted () {
    const price = await getMTBTPrice()
    this.mtbtPrice = Number(price.toFixed(3))
  },
  methods: {}
}
</script>

<style lang="less" scoped>
.sidebar {
  padding: 0 20px;
  box-sizing: border-box;
  top: 0;
  position: sticky;

  &-search-box {
    margin: 25px 0 0 0;
    width: 100%;
  }

  &-meta-coin-status {
    margin: 25px 0 0 0;
  }

  &-top-weekly-creators {
    margin: 25px 0 0 0;
  }

  &-login {
    margin-top: 25px;
  }
}
</style>
