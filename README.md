# CanalSharp

## �ع�����

Ŀǰ�ع��İ汾�Ѿ���ȫ���Ǿɰ汾�������ܸ��ߣ������������ʵ���˾ɰ汾δʵ�ֵĲ��ֹ��ܡ�

English README.md  Will be provided after the refactoring is complete.

| Task                | Status   |
| ------------------- | ------ |
| protobuf 3 Э������ | ����� |
| �Խ� Canal          | ����� |
| ���ݶ��ķ�װ        |        |
| ��Ⱥ֧��(�ȱ�)      |        |
| ���ݷ��͵�Kafka     |        |
| ���ݷ��͵�Redis     |        |

## ��������

>�Ⱦ���������װJava��������Ҫʹ�õ����ݿ⿪��binlog

### 1.���� Canal Server

��1���������µ� Canal Server https://github.com/alibaba/canal/releases/latest, ���� `canal.deployer-�汾��-SNAPSHOT.tar.gz` �ļ�

��2������

�༭�ļ� `conf/example/instance.properties`

���� MySql ��ַ��`canal.instance.master.address=`

���� MySql �û���`canal.instance.dbUsername=`

���� MySql ���룺`canal.instance.dbPassword=`

��3������
  ���� `bin` Ŀ¼���������ϵͳѡ��ű����С�

### 2.ʹ��

````csharp
//��ʼ����־
using var loggerFactory = LoggerFactory.Create(builder =>
{
    builder
        .AddFilter("Microsoft", LogLevel.Debug)
        .AddFilter("System", LogLevel.Information)
        .AddConsole();
});

//��������
var conn=new SimpleCanalConnection(new SimpleCanalConnectionOptions(Canal Server ��ַ,�˿� Ĭ�� 11111,ClientId �Զ���), loggerFactory.CreateLogger<SimpleCanalConnection>());

//���ӵ� Canal Server
await conn.ConnectAsync();
//������Ҫ���������
await conn.SubscribeAsync();
while (true)
{
    //��ȡ����
    var msg = await conn.GetAsync(1024);
    await Task.Delay(300);
}
````

>����ϸ���ĵ������ع���ɺ��ṩ
