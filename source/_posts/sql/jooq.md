https://www.jooq.org/doc/3.9/manual/#Overview

C

R

U

D

## 插入或更新
如果没有就插入，如果有则更新


## 判断某个字段是否为空
```java
step.and(TbkGoods.TBK_GOODS.COUPON_INFO.length().notEqual(0));
```