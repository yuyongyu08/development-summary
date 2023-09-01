# 列表渲染的key

key的作用？



用数组的index作为key有什么问题？



sameVnode的作用是判断两个节点是否相同，判断相同的根据是key值，tag(标签)，isCommit(注释),是否input的type一致等等，这种方法有点瑕疵，面对v-for下的key值使用index的情况，可能也会判断是可复用节点。 建议别使用index来作为key值。



