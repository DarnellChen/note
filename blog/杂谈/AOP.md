# Spring AOP

## AOP����

Aspect Oriented Programming��AOP��

���������̣���ͬҵ���������ڲ����޸�ԭ������߼����������ͨ������׷���µĴ����ܣ�

Object Oriented Programming��OOP��

��������̣������������ƣ�

AOP���ܵ�Ӧ�ó�����
- ׷���������
- ׷���쳣��־��¼

## ����ʾ��
- ����ͬ�Ĵ����װ��һ�����

	public class Bean{
		public void faction(){
			/*��ͬ������߼�����*/
		}
	}
	
- ׷��AOP���ã�����ͬ������õ�Ŀ�귽����

	aop.xml:
	
	/*xml��������ͬMyBatis*/
	<!-- 1��AOP���ã�����ͬ�����������õ�����Ŀ������ķ����� -->
	<bean id="AOPID" class = "��ͬ��������İ���.����" ></bean>
	
	<aop:config>
		<aop:aspect ref="AOPID">
			<aop:before method="��ͬ��������� ����Ŀ�귽��֮ǰ ���õķ���" pointcut="within(����) ����㣬Ŀ��ķ���"/>
			<!-- within �е����Ϳ�����д��������cn.clv.note.controller..* ���÷�ΧΪ�ð������Ӱ� -->
			<aop:after method=""/>
		</aop:aspect>
	</aop:config>
	

ע��ķ���

	aop.xml��
	
	/* xml ��������ͬMyBatis */
	<!-- ע��AOP���� -->
	<context:component-scan base-package="��ͬ����İ���" />
	<!-- ����AOPע���ǵ�ʹ�ã�����@Aspect��@Before��@After -->
	<aop:aspectj-autoproxy />
	
	//��װ��ͬ��������
	@Component//ɨ�裬�ȼ���<bean>����
	@Aspect//�ȼ���<aop:aspect> ����
	public class Bean{
		//�ȼ���<aop:before>����
		//��Ŀ�귽��ִ��ǰ����ִ�и÷���
		@Before("within()")
	}
	
### �����

����ָ��Ŀ�������������Spring�ṩ�˼���������ʽ

- �����޶����ʽ

	����ָ��ĳ������в��ַ���׷�ӹ�ͬ��������
	execution�����η�����������	������	�׳��쳣��

