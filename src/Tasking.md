背景
- 所有商品都有一个SellIn值，这是商品距离过期的天数，最好在这么多天内卖掉
- 所有商品都有一个Quality值，代表商品的价值
- 商品的SellIn值和Quality值，她们每天发生变化

商品的价格规则说明如下：
- 商品的价值永远不会小于0， 也永远不会超过50
- 普通商品每过一天价值会下滑1点，一旦过了保质期，价值就以双倍的速度下滑
- 后台门票（Backstage pass）是一种特殊商品：
    - 越接近演出日，商品的价值反而上升
    - 在演出前10天，价值每天上升2点
    - 演出前5天，价值每天上升3点
    - 一旦过了演出日，价值就马上变成0
    
Tasking
- GIVEN: 给定价格0 WHEN: 创建商品 THEN: 创建成功
- GIVEN: 给定价格50 WHEN: 创建商品 THEN: 创建成功
- GIVEN: 给定价格-1 WHEN: 创建商品 THEN: 创建失败 得到异常最低金额0
- GIVEN: 给定价格51 WHEN: 创建商品 THEN: 创建失败 得到异常最高金额50
- GIVEN: 普通商品初始价格0，保质期1 WHEN: 1天后查看价格 THEN: 价格为0
- GIVEN: 普通商品初始价格1，保质期1 WHEN: 1天后查看价格 THEN: 价格为0
- GIVEN: 普通商品初始价格1，保质期5 WHEN: 5天后查看价格 THEN: 价格为0
- GIVEN: 普通商品初始价格10，保质期10 WHEN: 5天后查看价格 THEN: 价格为5
- GIVEN: 普通商品初始价格10，保质期5 WHEN: 6天后查看价格 THEN: 价格为3
- GIVEN: 普通商品初始价格10，保质期5 WHEN: 8天后查看价格 THEN: 价格为0
- GIVEN: 后台门票初始价格0，保质期20 WHEN: 5天后查看价格 THEN: 价格为10
- GIVEN: 后台门票初始价格0，保质期20 WHEN: 15天后查看价格 THEN: 价格为35
- GIVEN: 后台门票初始价格20，保质期1 WHEN: 1天后查看价格 THEN: 价格为0
- GIVEN: 后台门票初始价格20，保质期20 WHEN: 19天后查看价格 THEN: 价格为50
