# Spring AOP

## AOP概念

Aspect Oriented Programming（AOP）

面向切面编程（共同业务处理，可以在不用修改原有组件逻辑代码情况下通过配置追加新的处理功能）

Object Oriented Programming（OOP）

面向对象编程（对象分析和设计）

AOP可能的应用场景：
- 追加事务控制
- 追加异常日志记录

## 入门示例
- 将共同的处理封装成一个组件

	public class Bean{
		public void faction(){
			/*共同处理的逻辑代码*/
		}
	}
	
- 追加AOP配置，将共同组件作用到目标方法上

	aop.xml:
	
	/*xml声明定义同MyBatis*/
	<!-- 1、AOP配置，将共同处理的组件作用到所有目标组件的方法上 -->
	<bean id="AOPID" class = "共同处理组件的包名.类名" ></bean>
	
	<aop:config>
		<aop:aspect ref="AOPID">
			<aop:before method="共同处理组件内 想在目标方法之前 调用的方法" pointcut="within(类型) 切入点，目标的方法"/>
			<!-- within 中的类型可以填写包名：如cn.clv.note.controller..* 作用范围为该包及其子包 -->
			<aop:after method=""/>
		</aop:aspect>
	</aop:config>
	

注解的方法

	aop.xml：
	
	/* xml 声明定义同MyBatis */
	<!-- 注解AOP配置 -->
	<context:component-scan base-package="共同处理的包名" />
	<!-- 开启AOP注解标记的使用，例如@Aspect，@Before，@After -->
	<aop:aspectj-autoproxy />
	
	//封装共同处理的组件
	@Component//扫描，等价于<bean>定义
	@Aspect//等价于<aop:aspect> 定义
	public class Bean{
		//等价于<aop:before>定义
		//在目标方法执行前，先执行该方法
		@Before("within()")
	}
	
### 切入点

用于指定目标组件及方法。Spring提供了几种切入表达式

- 方法限定表达式

	可以指定某个组件中部分方法追加共同方法功能
	execution（修饰符？返回类型	方法名	抛出异常）

