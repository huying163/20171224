maxflow算法
1.基本思想：标号法，预流推进
通过对maxflow判定条件的分析，可知maxflow需要满足两个条件：可行流，无增广路径。这两个基本思想是通过不同的思考角度来解决最大流问题的。
标号法是在满足可行流前提下，逐步迭代使得无增广路径；而预流推进则反其道而行之，在保证没有增广路径的前提下，逐步迭代使得分配可行。

2.应用场景：一种基于增广路径的求解最大流最小割的算法,算完之后，会自动完成最小割集的构造.

3.算法步骤：
  （1) "增长"阶段：搜索树S和T扩展节点，直到两树相遇，得到一条由源点s到汇点t的增广路径。
   (2) "增广"阶段：根据找到的增广路径将搜索树拆分为子树或森林。
   (3) "领养"阶段：搜索树S和T重新构建。
   
4.伪代码：
  initialize:   S = {s},T = {t}, A = {s,t}, O = 空集
  while true
            grow S or T to find an augmenting path
                 P from s to t
            if P = 空集 terminate
            augment on P
            adopt orphans
   end while
    
5.接口：
input:
List<Field> maxflow_List = record.get("/maxflow_array")。getValueAsList();
int source = record.get("/source").getValueAsInteger();
int sink = record.get("/sink").getValueAsInteger();

output:
record.set("/flowsize", Field.create(flowsize));
record.set("/flow",Field.create(flowfied));
