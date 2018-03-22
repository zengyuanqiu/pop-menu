# pop-menu

用法
```vue
<popup-menu slot='right' 
	bgColor='#49484B' 
  :isShow='popupShow'
  @changeShowVal='popupShow=false'>
  <mt-button icon="more" @click='popupShow=!popupShow'></mt-button>
  <ul slot='menu' class='menu-wrap'>
    <li class='menu-item'>发起群聊</li>
    <li class='menu-item'>添加好友</li>
    <li class='menu-item'>设置</li>
  </ul>
</popup-menu>
```
bgColor: 背景色（string) 默认白色<br>
isShow: 显示/隐藏 默认false<br>
@changeShowVal: 通知父组件改变了popupShow的值为false
