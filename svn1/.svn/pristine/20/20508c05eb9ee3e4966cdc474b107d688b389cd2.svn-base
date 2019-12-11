<script>
export default {
  name: 'MenuItem',
  functional: true,
  props: {
    icon: {
      type: String,  
      default: ''
    },
    title: {
      type: String,
      default: ''
    }
  },
  render(h, context) {
    //console.log(context.props);//打印每个路由的icon,title
    const { icon, title } = context.props
    const vnodes = []

    if (icon) {
      //这里判断导出的svg方式
      vnodes.push(<svg-icon icon-class={icon}/>)
    }
    //这里绑定title
    if (title) {
      vnodes.push(<span slot='title'>{(title)}</span>)
    }
    return vnodes
  }
}
</script>
