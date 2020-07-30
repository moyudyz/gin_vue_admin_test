<template>
  <div class="search-component">
    <transition name="el-fade-in-linear">
      <div v-show="show" class="transition-box" style="display: inline-block; ">
        <el-select
          v-model="value"
          filterable
          placeholder="请选择"
          @blur="hiddenSearch"
          @change="changeRouter"
        >
          <el-option
            v-for="item in routerList"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          />
        </el-select>
      </div>
    </transition>
    <div :style="{display:'inline-block'}">
      <i class="el-icon-search search-icon" @click="show = !show" />
    </div>
  </div>
</template>
<script>
import { mapGetters } from 'vuex'

export default {
  name: 'SearchComponent',
  data() {
    return {
      value: '',
      show: false
    }
  },
  computed: {
    ...mapGetters('router', ['routerList'])
  },
  methods: {
    changeRouter() {
      this.$router.push({ name: this.value })
      this.value = ''
    },
    hiddenSearch() {
      this.show = false
    }
  }
}
</script>
<style lang="scss">
.search-component {
  display: inline-block;
  .el-input__inner {
    border: none;
    border-bottom: 1px solid #606266;
  }
  .el-dropdown-link {
    cursor: pointer;
  }
  .search-icon {
    font-size: 20px;
    margin-right: 14px;
    display: inline-block;
    vertical-align: middle;
    box-sizing: border-box;
    color: #606266;
  }
  .dropdown-group {
    min-width: 100px;
  }
}
</style>
