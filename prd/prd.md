# () Operators Optimization
1. 增加对括号操作的支持，用于改变操作的优先级, e.g.
 - (x AND y) OR z 表示先计算 x AND y 的结果，再与 z 进行 OR 操作
 - x AND (y OR z) 表示先计算 y OR z 的结果，再与 x 进行 AND 操作
2. 括号操作可以嵌套使用, e.g.
 - ((x AND y) OR z) AND w 表示先计算 x AND y 的结果，再与 z 进行 OR 操作，最后与 w 进行 AND 操作
3. 语法中增加规则 相应的括号操作的说明，以 BO 序列命名（括号操作）。

# IN and OF  Optimization

1. 其中 IN OF 操作改成 INOF。 
2. IN 和 INOF 操作都用于集合判断, e.g.
 - x BEF/5 IN(a,b,c) 的含义中 在 x 出现在a的位置之前的5个位置内，b的位置之前5个位置内，c的位置之前5个位置内。
 - x BEF/5 OF(a,b,c) 的含义中 在 x 出现在a的位置之前的5个位置内或b的位置之前5个位置内或c的位置之前5个位置内。
3. 单独使用 IN 和 INOF 为语法错误, e.g.
 - IN(a,b,c) AND ... 语法错误
 - OF(d,e,f) OR .... 语法错误
4. 语法中增加规则 相应的 IN 和 INOF 操作的说明，以 SO 序列命名（集合操作）。



# LEN and SIZE Optimization
1. 增加LEN操作，用于计算出现单词的个数, e.g.
    - LEN/3 表示判断的字符串中的单词数量少于等于3
    - LEN/5-10 表示判断的字符串中的单词数量在5到10之间

2. LEN操作可以和其他操作结合使用, e.g.
    - LEN/3 AND x BEF/5 y 表示字符串中单词数量少于等于3且x在y之前5个位置内
    - NOT LEN/2 表示判断的字符串中的单词数量大于2
    - NOT LEN/5-10 表示判断的字符串中的单词数量不在5到10之间

3. 增加SIZE操作，用于计算字符串的字节数, e.g.
    - SIZE/3 表示判断的字符串的字节数少于等于3
    - SIZE/5-10 表示判断的字符串的字节数在5到10之间
    - SIZE操作可以和其他操作结合使用, e.g.
    - SIZE/3 AND x BEF/5 y 表示字符串的字节数少于等于3且x在y之前5个位置内
    - NOT SIZE/2 表示判断的字符串的字节数大于2
    - NOT SIZE/5-10 表示判断的字符串的字节数不在5到10之间

3. 语法中增加规则 相应的 LEN 和 SIZE 操作的说明，以 LO 序列命名（长度操作）。



# Position Operator Optimization
1. 在位置操作中增加对 * 号的支持，表示任意位置, e.g.
 - x BEF/* y 表示 x 在 y 之前的任意位置
 - x AFT/* z 表示 x 在 z 之后的任意位置
 - x NEAR/* y 表示 x 在 y 的任意位置附近

2. 增加位置区间的支持, e.g.
 - x BEF/3-5 y 表示 x 在 y 之前的3到5个位置内
 - x AFT/2-4 z 表示 x 在 z 之后的2到4个位置内

3. 语法中增加规则 相应的位置操作的说明，以 PP 序列命名（位置操作）。

# XOR Operator 
1. 增加 XOR 操作，用于表示异或关系, e.g.
    - x XOR y 表示 x 和 y 其中一个出现但不能同时出现
2. XOR 操作可以和其他操作结合使用, e.g.
    - (x XOR y) AND z 表示 x 和 y 其中一个出现且 z 出现
    - NOT (x XOR y) 表示 x 和 y 要么都出现要么都不出现

3. 类似OR 和 AND，操作， 支持复杂的 XOR 关系, e.g.
    - (x XOR y) OR (a XOR b) 表示 x 和 y 其中一个出现或 a 和 b 其中一个出现
    - (x XOR y) AND (a XOR b) 表示 x 和 y 其中一个出现且 a 和 b 其中一个出现
    - (x NEAR y) XOR (a BEF b) 表示 x 在 y 附近出现或 a 在 b 之前出现，但不能同时满足这两个条件

4. 在运算优先级上 XOR 和 OR 、AND 一样，支持括号操作来改变优先级。
5. 语法中增加规则 相应的 XOR 操作的说明，以 BO 序列命名（异或操作）。


# NOT Operator Enhancement
1. 增强 NOT 操作的功能，支持对更复杂表达式的否定, e.g.
 - NOT (x AND y) 表示 x 和 y 不同时出现
 - NOT (x OR y) 表示 x 和 y 都不出现
 - NOT (x BEF/5 y) 表示 x 不在 y 之前的5个位置内
2. NOT 操作可以嵌套使用, e.g.
 - NOT (x AND NOT y) 表示 x 出现且 y 不出现
 - NOT (NOT (x OR y)) 表示 x 或 y 至少有一个出现

# Delte Some Operator 
1. 删除冗余或不常用的操作符，以简化语法和提高处理效率, e.g.
 - 删除 WITHIN 、IMPLIES 操作符
