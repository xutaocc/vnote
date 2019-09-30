# mybatis

## mybatis使用介绍大全-YSOcean[链接](https://www.cnblogs.com/ysocean/tag/MyBatis详解系列/)

### mybatis 详解（八）------ 懒加载[链接](https://www.cnblogs.com/ysocean/p/7336945.html)
### mybatis 详解（九）------ 一级缓存、二级缓存



### 小问题总结
#### MyBatis中<if test=" ">标签条件不起作用[链接](https://www.cnblogs.com/sxdcgaq8080/p/9443023.html)
```
注意 要想使用 ==   仅仅需要将双引号和单引号的位置换一下即可!!! 

<update id="updateGoodsShelf" parameterType="java.lang.String">
        update
        integral_goods
        set
        <if test='shelfFlag == "1"'>
            shelf_flag = ${@com.pisen.cloud.luna.ms.jifen.base.domain.IntegralGoods@SHELF_ON}
        </if>
        <if test='shelfFlag == "0"'>
            shelf_flag = ${@com.pisen.cloud.luna.ms.jifen.base.domain.IntegralGoods@SHELF_OFF}
        </if>
        where
        uid
        IN
        <foreach collection="list" item="item" index="index" open="(" separator="," close=")">
            #{item}
        </foreach>
    </update>


```
