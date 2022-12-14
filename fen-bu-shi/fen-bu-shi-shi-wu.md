# 分布式事务

{% embed url="https://pdai.tech/md/arch/arch-z-transection.html" %}

## 分布式事务

微服务架构下，一个系统被拆分为多个小的微服务。每个微服务都可能存在不同的机器上，并且每个微服务可能都有一个单独的数据库供自己使用。这种情况下，一组操作可能会涉及到多个微服务以及多个数据库。举个例子：电商系统中，你创建一个订单往往会涉及到订单服务（订单数加一）、库存服务（库存减一）等等服务，这些服务会有供自己单独使用的数据库。

<img src="../.gitbook/assets/file.drawing (3).svg" alt="" class="gitbook-drawing">

那么如何保证这一组操作要么都执行成功，要么都执行失败呢？&#x20;

这个时候单单依靠数据库事务就不行了！我们就需要引入 **分布式事务** 这个概念了！&#x20;

实际上，只要跨数据库的场景都需要用到引入分布式事务。比如说单个数据库的性能达到瓶颈或者数据量太大的时候，我们需要进行 分库。分库之后，同一个数据库中的表分布在了不同的数据库中，如果单个操作涉及到多个数据库，那么数据库自带的事务就无法满足我们的要求了。

<img src="../.gitbook/assets/file.drawing (2).svg" alt="" class="gitbook-drawing">

一言蔽之，分布式事务的终极目标就是保证系统中多个相关联的数据库中的数据的一致性！&#x20;

那既然分布式事务也属于事务，理论上就应该准守事物的 ACID 四大特性。但是，考虑到性能、可用性等各方面因素，我们往往是无法完全满足 ACID 的，只能选择一个比较折中的方案。

&#x20;针对分布式事务，又诞生了一些新的理论。
