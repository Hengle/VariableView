# VariableView
### 本代码的功能是演示一种视野处理方式，可以满足的需求有：
1. 每个地图可以单独设置不同的格子大小，格子大小影响视野精度，也会对内存和计算量产生影响。
2. 每个实体可以设置自己的可视距离和占据的体积，其单位都是游戏内的真实单位而不是格子数。
3. 可以实现动态的更改实体的可视距离以便满足获得千里眼道具后可以看的更远等类似需求。

### 实现原理
* 将地图划分成等大的格子，每个格子内存储位于当前格子内的实体对象链表和正在关注当前格子的实体链表。
* 实体对象则存储它正在关注的所有格子以及它所占据的格子,如果是非质点实体那么它将同时存在于多个格子上。
* 实体移动时更改自己所在的格子，触发旧格子内的实体离开事件和新格子的实体进入事件，对应的格子会把事件向注册的所有实体广播出去，实体移动后更新自己的关注列表，找出不再关注的格子，把自己从对应格子反注册，找出新关注的格子，将自己注册进去(此处用了一个快速求两个集合的并集和差集的算法，见 `Utils.cs`)

### 运行效果图
![image](https://github.com/easy66/VariableView/blob/master/Code.png)
![image](https://github.com/easy66/VariableView/blob/master/Result.png)