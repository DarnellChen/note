# Spring + Mybatis 事务操作

主要是针对增删改的数据修改操作

需要保证两个及以上的sql进行操作都能成功

## 作用

保障一组数据库SQL操作的完整性。

## 项目中的事务

默认每个Dao方法都是一个独立事务，如果Service方法使用两个Dao方法处理，无法保障Service方法的完整性。


## 实现
	
	//通常结构
	//采用事务，保证service处理完整性
	public void service(){
		try{
			//开启事务
			/*多个Dao方法*/
			Service.shareNote()
			//提交事务
		}catch(){
			//异常回滚事务
		}
	}
	
	
###	spring事务处理

Spring提供了事务管理的封装，不同技术提供的封装组件不同，例如JDBC和MyBatis采用DataSourceTransactionManager组件封装了事务commit和捕获异常后rollback。
Spring底层借助了 **AOP机制** 将DataSourceTransactionManager作用到业务方法上去。
（基于配置方式）

创建配置文件transaction.xml
	
	/*xml声明定义同MyBatis*/
	<!-- 1、定义事务管理Bean-->
	<bean id = "txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
		<property name = "dataSource" ref = "自定义的dbcp组件DataSource的id名">
		</property>
	</bean>
	
	<!-- 2、通过配置将txManager作用到Service方法上 -->
	<!-- 开启@Transactional 事务标记-->
	<tx:annotation-driven transaction-manager="txManager" />

	<!-- 2的另一种实现方式-->
	<tx:advice id="txAdvice" transaction-manager="txManager" >
		<tx:attributes>
			<tx:method name="faction*" read-only="true" />
			<tx:method name="fa*" />
		</tx:attributes>
	</tx:advice>


在service类/方法前上

	//带该标记的方法，会采用DataSourceTransactionManager控制事务
	@Transactional
	public void serviceClass{
	
	}

## 总结

- <bean>定义DataSourceTransactionManager
- 开启@Transactional注解<tx:annotation-driven transaction-manager="txManager" />
- 在业务组件类前或方法前使用@Transactional