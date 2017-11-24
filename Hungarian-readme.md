1.概述
  匈牙利算法(Hunggarian Algorithm)是一种组合优化算法(combinatorial optimization algorithm)，用于求解指派问题。
应用场景：可以找到开销最小的方案

2.匈牙利算法简要步骤：
  step-1:对开销矩阵的各行进行操作：找出每一行中值最小的元素，然后把该行所有元素都减去这一最小值  
  step-2:对开销矩阵的各列进行操作：找出每一列值最小的元素，然后把该列所有元素都减去这这一最小值
  step-3:用尽量少的横线或竖线覆盖矩阵中的所有0
  step-4:从上一步中未被覆盖的元素中找到最小值，然后把这些元素都减去这一小值，给直线交叉点的元素加上这一最小值
  step-5:重复step-3和step-4，直到所有任务都被分配


3.核心思想：增广路径(augment path)
基本模式：初始时最大匹配为空
1 while 找到增广路径 do
2       把增广路径加入到最大匹配中去

4.接口
Input:
List<Field> match_List = record.get("/match_array").getValueAsList();

Output:
record.set("/sum_value", Field.create(ret));
record.set("/xylist",Field.create(xylist));
