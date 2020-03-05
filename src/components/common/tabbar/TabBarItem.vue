<template>
  <div class="tab-bar-item" @click="itemClick">
    <div v-if="!isActive"><slot name="item-icon"></slot></div>
    <div v-else><slot name="item-icon-active"></slot></div>
    <div :style="activeStyle"><slot name="item-text"></slot></div>
  </div>

</template>

<script>
    export default {
        name: 'TabBarItem',
        props: {
          path: String,//用string字符串的话，在用tabbar是，就不用加上：冒号————其他则要加上：冒号
          activeColor: {
              type:String,
              default: 'red'      //默认没有传值时是红色
          }
        },
        data() {
            return{
                // isActive: true
            }
        },
        computed: {
            isActive() {
                //判断谁处于活跃
                //判断当前的path是否跟获取的path一致，一致则为true，否则为false
                //   /home    ->   item1(/home)    =   true
                //   /category  ->   item1(/category)  =   false
                //   /profile     ->   item1(/profile)     =   false
                //   /cart   ->   item1(/cart)   =   false
                return this.$route.path.indexOf(this.path) !== -1

            },
            activeStyle() {
                //上面的判断这里来使用
                //判断谁否成为活跃，是为true，三目运bn算符
                return this.isActive ? {color: this.activeColor} : {}
            }
        },
        methods: {
            itemClick() {
                //想要用返回就用————push
                // console.log('itemClick');
                this.$router.replace(this.path)
                //不想要用返回就用————replace
            }
        }
    }
</script>

<style scoped>

  .tab-bar-item {
    flex: 1;
    text-align: center;
    height: 49px;
    font-size: 12px;
  }

  .tab-bar-item img {
    width: 24px;
    height: 24px;
    margin-top: 3px;
    vertical-align: middle;
    margin-bottom: 2px;
  }

</style>
