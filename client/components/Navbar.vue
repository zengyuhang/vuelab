<template>
  <div class="vux-header">
    <div class="vux-header-left">
      <a class="vux-header-back" @click.preventDefault v-show="options.showBack"  @click="onClickBack">{{options.backText}}</a>
      <div class="left-arrow" @click="onClickBack" v-show="options.showBack" ></div>
      <slot name="left"></slot>
    </div>
    <h1 class="vux-header-title" @click="$emit('on-click-title')"><span v-show="title" >{{title}}</span><slot></slot></h1>
    <div class="vux-header-right">
      <slot name="right"></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Object,
      default () {
        return {
          showBack: true,
          backText: 'Back',
          preventGoBack: false
        }
      }
    },
    title: String,
  },
  methods: {
    onClickBack () {
      if (this.options.preventGoBack) {
        this.$emit('on-click-back')
      } else {
        history.back()
      }
    }
  }
}
</script>

<style>
:root{
  --background-color: #35495E;
  --text-color: white;
}
.vux-header {
  position: relative;
  padding: 3px 0;
  box-sizing: border-box;
  background-color:var(--background-color);
}
.vux-header .vux-header-title,.vux-header h1 {
  margin: 0 88px;
  margin-left: 100px;
  line-height: 40px;
  text-align: center;
  height: 40px;
  font-size: 18px;
  font-weight: 400;
  width: auto;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  color: var(--text-color);
}
.vux-header .vux-header-title > span {
  display: inline-block;
}
.vux-header .vux-header-left,.vux-header .vux-header-right {
  position: absolute;
  top: 14px;
  display: block;
  font-size: 14px;
  line-height: 21px;
  color: var(--text-color);
}
.vux-header .vux-header-left a,.vux-header .vux-header-left button,.vux-header .vux-header-right a,.vux-header .vux-header-right button {
  float: left;
  margin-right: 8px;
  color: var(--text-color);
}
.vux-header .vux-header-left a:active,.vux-header .vux-header-left button:active,.vux-header .vux-header-right a:active,.vux-header .vux-header-right button:active {
  opacity: .5
}
.vux-header .vux-header-left {
  left: 18px
}
.vux-header .vux-header-left .vux-header-back {
  padding-left: 16px
}
.vux-header .vux-header-left .left-arrow {
  position: absolute;
  width: 30px;
  height: 30px;
  top: -5px;
  left: -5px;

  &:before {
    content: "";
    position: absolute;
    width: 12px;
    height: 12px;
    border: 1px solid var(--text-color);
    border-width: 1px 0 0 1px;
    transform: rotate(315deg);
    top: 8px;
    left: 7px;
  }
}
.vux-header .vux-header-right {
  right: 15px
}
.vux-header .vux-header-right a,.vux-header .vux-header-right button {
  margin-left: 8px;
  margin-right: 0
}
.vux-header .vux-header-right .vux-header-more:after {
  content: "\2022\0020\2022\0020\2022\0020";
  font-size: 16px;
}
.vux-header-fade-in-right-enter {
  animation: fadeinR .5s;
}
.vux-header-fade-in-left-enter {
  animation: fadeinL .5s;
}
@keyframes fadeinR{
  0%{opacity:0;transform:translateX(80px);}
  100%{opacity:1;transform:translateX(0);}
}
@keyframes fadeinL{
  0%{opacity:0;transform:translateX(-80px);}
  100%{opacity:1;transform:translateX(0);}
}
</style>
