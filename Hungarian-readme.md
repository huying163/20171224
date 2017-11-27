1.概述
  匈牙利算法(Hunggarian Algorithm)是一种组合优化算法(combinatorial optimization algorithm)，用于求解指派问题。
应用场景：可以找到开销最小的方案

2.匈牙利算法简要步骤：

  step-1:对开销矩阵的各行进行操作：找出每一行中值最小的元素，然后把该行所有元素都减去这一最小值 
  
  完成后矩阵的每一行至少会出现一个0.假如a1,b4,c2,d3是开销矩阵的最小值，则开销矩阵在完成本项操作后变成
  
      \begin{bmatrix} 0 & a_2-a_1&a_3-a_1&a_4-a_1 \\ 
      b_1-b_4&b_2-b_4&b_3-b_4&0\\
      c_1-c_2&0&c_3-c_2&c_4-c_2\\
      d_1-d_3&d_2-d_3&0&d_4-d_3
      \end{bmatrix}.
  

  step-2:对开销矩阵的各列进行操作：找出每一列值最小的元素，然后把该列所有元素都减去这这一最小值
  
  step-3:用尽量少的横线或竖线覆盖矩阵中的所有0
  
  step-4:从上一步中未被覆盖的元素中找到最小值，然后把这些元素都减去这一小值，给直线交叉点的元素加上这一最小值
  
  step-5:重复step-3和step-4，直到所有任务都被分配


3.核心思想：增广路径(augment path)
基本模式：初始时最大匹配为空
1 while 找到增广路径 do
2       把增广路径加入到最大匹配中去

伪代码
    1  假设我们为N个A，匹配M个B，那么   

    2  for i:=1 to n do

    3      fillchar(p,sizeof(p),0);

    4      if can(i) then inc(ans) 可以匹配就加入答案

    5  匹配过程 (can(i)):

    6  if p[i] then exit(false) 如果p[i]已经赶过别人了，就不能再被赶了，不然会死循环

    7  p[i]:=true;

    8  for j:=1 to m do 从头 开始找一个B来匹配

    9  if (b[j]=0) or (can(b[j])) then

    10 若B中j这个位置为空，或者可以赶走别人，就占有这里

    11    begin

    12        b[j]=i;

    13       exit(true);匹配成功

    14    end;

    15 exit(false);匹配失效


4.接口
Input:
List<Field> match_List = record.get("/match_array").getValueAsList();

Output:
record.set("/sum_value", Field.create(ret));

record.set("/xylist",Field.create(xylist));

5.举例
假设有三位工人A，B和C，需要分配他们每人完成一件工作；对于不同的工作他们索要不同的工钱，如下表所示。问题就是要找到一套开销最小的指派方案。

|Tables     | 扫地         | 擦窗户      |    清理浴室    |
|-----------|:-----------:|:----------:|--------------:|
|     A     |     120元   |   300元     |   300元       |
|     B     |     300元   |   120元     |   300元       |
|     C     |     300元   |   300元     |   120元       |

使用匈牙利方法可以找到开销最小的方案，即A负责扫地，B负责擦窗户，C负责清理浴室，总开销为360元。



