# 成绩

队伍：IOT_TEAM(成渝赛区)

初赛： 0.1152 (成渝rank 1/总榜rank 3)

复赛A1： 0.6748 (成渝rank 1/总榜rank 1)

复赛A2： 2.2934 (成渝rank 1/总榜rank 7)

复赛B：3.1988(成渝rank 2/总榜rank 6)

决赛A：300.2459(总榜rank 3)

决赛B：263.7404(总榜rank 5)

上分总结及分析(陆续填坑)：https://blog.csdn.net/u011627998/article/details/106446915

# 初赛/复赛 寻找有向图中的环路

初赛：5+3反向搜索存储三层路径(二级内存存储路径)，正向递归搜索（第四个点时4+1/4+2/4+3得到5/6/7环）

复赛A：5+3反向搜索存储三层路径(二级内存存储路径)，正向for循环套娃(0+3/1+3/2+3/3+3/4+3得到3/4/5/6/7环)，引用robin_map库替换unordered_map，正式代码从2327行起

复赛B：5+3.5反向搜索存储三层路径(二级内存存储路径)，反向第四层记录可达性标记，正向for循环套娃(0+3/1+3/2+3/3+3/4+3/5+3得到3/4/5/6/7/8环)

# 决赛 计算有向图的节点中介中间性

① 第一组数据为菊花图，利用对出度1入度0节点计算结果并到其后继节点计算，第一组线上数据90S

② 第一组数据度数不均匀，为了保障邻接表遍历访问尽量连续，构图后对图进行bfs重构邻接表，使得相邻节点在邻接表中的位置尽量相邻，这个trick使得线下数据一优
化至8S

③ 官方数据dis较小，优先队列中可只存dis，大幅度减少队列调整规模，利用哈希/数组根据阈值切换vector映射，vector中存储dis对应的id以供遍历。（线上A榜 
740->480）

④ 根据dis较小，尽量选取符合位数的数据类型进行搜索，线上dis不超过65536，所有dis及金额均可以采用short存储。（线下数据2提升20S，决赛线上提升10S）

⑤ 搜索时存储前驱点的数组uint32 P[MAXN][150] 采用二维而不是两个一维线下数据二可提升20S，第二维的规模尽量小减少page fault，决赛修改线上提升2S


