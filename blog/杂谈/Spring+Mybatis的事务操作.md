# Spring + Mybatis �������

��Ҫ�������ɾ�ĵ������޸Ĳ���

��Ҫ��֤���������ϵ�sql���в������ܳɹ�

## ����

����һ�����ݿ�SQL�����������ԡ�

## ��Ŀ�е�����

Ĭ��ÿ��Dao��������һ�������������Service����ʹ������Dao���������޷�����Service�����������ԡ�


## ʵ��
	
	//ͨ���ṹ
	//�������񣬱�֤service����������
	public void service(){
		try{
			//��������
			/*���Dao����*/
			Service.shareNote()
			//�ύ����
		}catch(){
			//�쳣�ع�����
		}
	}
	
	
###	spring������

Spring�ṩ���������ķ�װ����ͬ�����ṩ�ķ�װ�����ͬ������JDBC��MyBatis����DataSourceTransactionManager�����װ������commit�Ͳ����쳣��rollback��
Spring�ײ������ **AOP����** ��DataSourceTransactionManager���õ�ҵ�񷽷���ȥ��
���������÷�ʽ��

���������ļ�transaction.xml
	
	/*xml��������ͬMyBatis*/
	<!-- 1�������������Bean-->
	<bean id = "txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
		<property name = "dataSource" ref = "�Զ����dbcp���DataSource��id��">
		</property>
	</bean>
	
	<!-- 2��ͨ�����ý�txManager���õ�Service������ -->
	<!-- ����@Transactional ������-->
	<tx:annotation-driven transaction-manager="txManager" />

	<!-- 2����һ��ʵ�ַ�ʽ-->
	<tx:advice id="txAdvice" transaction-manager="txManager" >
		<tx:attributes>
			<tx:method name="faction*" read-only="true" />
			<tx:method name="fa*" />
		</tx:attributes>
	</tx:advice>


��service��/����ǰ��

	//���ñ�ǵķ����������DataSourceTransactionManager��������
	@Transactional
	public void serviceClass{
	
	}

## �ܽ�

- <bean>����DataSourceTransactionManager
- ����@Transactionalע��<tx:annotation-driven transaction-manager="txManager" />
- ��ҵ�������ǰ�򷽷�ǰʹ��@Transactional

# ��������isolation

һ�����Ĭ�ϸ��뼶�𣬼���ΪREAD_COMMITED ����ԭ������Ϊ������Ĳ�����
���������ݿ�������벢�������ײ���������ö������¶�ʧ�����⣩

����������ǲ��ø��뼶�����ã��������������������뿪��

@Transactional�ṩ������뼶��

@Transactional(isolation=Isolation.***)

- READ_UNCOMMITTED ��δ�ύ
- READ_COMMITTED �����ύ
- REPEATABLE_READ ���ظ���
- SERIALIZABLE ���л��������ŶӲ�����

����Խ�߰�ȫ��Խ�ã����ǲ�����������Խ�͡�

���ֹ���/��������