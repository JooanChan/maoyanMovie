<template>
  <header>
    <nav class="nav">
      <ul class="wrap">
        <li class="tab" :class="{active: item.name === navTitle}" v-for="item in nav" :key="item.id">
          <router-link :to="{name: item.mark}">{{item.name}}</router-link>
        </li>
      </ul>
    </nav>
    <div class="city">
      <router-link class="local" :to="{name: 'city'}">{{locate.city}}</router-link>
    </div>
    <div class="search">
      <router-link :to="{name: 'searchMovie'}">
        <icon class="icon" type="search"></icon>
      </router-link>
    </div>
  </header>
</template>

<script>
import { Icon } from 'vux'
import { mapState } from 'vuex'

export default {
  name: 'innerHeader',
  data () {
    return {
      nav: [ // 导航
        {
          name: '热映',
          mark: 'hot'
        },
        {
          name: '待映',
          mark: 'await'
        }
      ]
    }
  },
  computed: {
    ...mapState({
      locate: state => state.locate // 当前城市
    }),
    navTitle () {
      return /hot/.test(this.$route.path) ? '热映' : '待映'
    }
  },
  methods: {

  },
  components: {
    Icon
  },
  mounted () {
  }
}
</script>

<style lang="less" scoped>
@import '../../../style/base';

header {
  height: 130 / @rem;
  background-color: #fff;
}
.nav {
  float: left;
  width: 100%;
  height: 130 / @rem;
}
.city {
  float: left;
  width: 180 / @rem;
  height: 130 / @rem;
  line-height: 130 / @rem;
  text-align: center;
  margin-left: -100%;
  .local {
    color: @cityC;
    &:after {
      content: '';
      position: relative;
      top: 8px;
      left: 5px;
      .triangle-bottom(12/@rem, #cacaca);
    }
  }
}
.search {
  float: left;
  width: 130 / @rem;
  height: 130 / @rem;
  line-height: 130 / @rem;
  margin-left: -130 / @rem;
  border-left: 1px solid @grey;
  text-align: center;
  .icon {
    font-size: 50 / @rem;
    color: @orange;
  }
}
.wrap {
  margin: 0 auto;
  overflow: hidden;
  width: 436 / @rem;
  .tab {
    float: left;
    width: 130 / @rem;
    height: 110 / @rem;
    line-height: 120 / @rem;
    margin: 0 44 / @rem;
    text-align: center;
    font-weight: bold;
    a {
      color: #8e8e8e;
    }
  }
  .active {
    border-bottom: 1px solid @orange;
    a {
      color: @orange;
    }
  }
}
</style>
