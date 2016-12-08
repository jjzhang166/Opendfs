Opendfs��һ����C/C++��д�ķֲ�ʽ�ļ��洢ϵͳ�������и߶��ݴ��߲�������������������չ����������Linux�ļ�ϵͳ���ļ���Ŀ¼�ṹ���ص㣻
������HDFS��һ��Opendfs��ȺҲ��DFSClient��Namenode��Datanode���ֽ�ɫ��ɣ�һ���ļ�����DFSClient�зֳɶ�����ݿ�洢����Ⱥ�ϣ���Datanode���𱣴���Щ���ݿ飬Namenode����ά���ļ��ɶ��ٸ�����ɣ���Щ�鱣�����ĸ�Datanode�ϵ�ӳ���ϵ����Ⱥ����ܹ���ͼ1ʾ��
![ͼ1](https://github.com/liaosanity/Opendfs/images/overall_architecture.png)
                                   ͼ1
# ����ɫ���ܽ������£�
 * Namenode��Ԫ���ݴ洢�ڵ㣬����Ԫ���ݵĹ��������ļ���Ŀ¼���ڼ�Ⱥ�еĴ洢�ṹ��ÿ���ļ���Ӧ�����ݿ��б������ݿ�洢����Щ���ݽڵ��ϣ��������ݽڵ�Ĵ��״̬�Լ��������Ķ�д���ȵȣ�ÿ��Ԫ���ݵĲ�����д��ɾ�������˸����ڴ棬�������һ��������־д�����ش��̵���־�ļ���editlog������д�����ǰ����������־��ͨ��paxosЭ��ͬ����������Ԫ���ݽڵ㣬��ĳ���趨ʱ��㣨checkpoint����ÿ��Ԫ���ݽڵ����ڴ��е�Ԫ����dump�����ش������ɾ����ļ���fsimage������ȷ��editlog�ļ������ڹ���Ԫ���ݽڵ��ÿ������������ͨ��fsimage��editlog�ļ���̬���ؽ�Ԫ���ݵ�ӳ���ϵ��
 * Datanode�����ݴ洢�ڵ㣬�����ļ����ݿ�Ĺ���ÿ�����ݿ齫���ļ�����ʽ�洢�������ļ�ϵͳ���������Կͻ��˵����ݿ��д��������ʱ��ע�ᵽ����Ԫ���ݽڵ㣬ͨ�����������ϱ���ʱ��Ԫ���ݽڵ�㱨�Լ��Ľ���״̬���磺ʣ��������С����ǰ���������������ǰ�洢�Ŀ����Լ����ݿ��Ƿ��𻵵ȣ�ͬʱ��������Ԫ���ݽڵ��ָ��紴�����ƶ���ɾ�����ݿ�ȡ�
 * DFSClient���ļ���д�նˣ����û��뼯Ⱥ��������Ҫ�ֶΣ��ṩ����Linux���ls��rm��rmr������Posix�ӿڵȣ������ļ��зֳɶ���������ݽڵ�д��ͨ����ȡ���Ը������ݽڵ�����ݿ飬�ϳ�һ���������ļ���Ӧ�ò㷵�ء�

# һЩ�ص㣺
 * �洢��Opendfs�е��ļ�����Ԫ��Ϣ���ļ����ݻ�ֱ�洢����HDFS��ͬ���ǣ��洢Ԫ��Ϣ��Namenode�������Ƕ�̨�������ȱ��ļܹ������������Ӽ�ͨ��PaxosЭ��ͬ����֤Ԫ���ݵ�����һ���ԣ�������ģ�ʹ����У�HDFS��һ��������һ���߳�����ɣ���Opendfs�ǲ���epoll�¼�����ģ�ͣ��Ӷ��������Ĳ�������Ч�ʡ�
 * �ļ��ڼ�Ⱥ�н�����һ����С�зֳɶ�����ݿ飨ÿ��Ĭ��256M�������ã�����ɢ�洢�ڸ���Datanode�ϣ�ÿ�����ݿ�ͨ����������洢�ڶ�̨Datanode�ϣ�ͨ���Զ��޸��𻵡���ʧ�ĸ������Ӷ���֤���ݿ�Ŀɿ��ԣ���HDFS�У�Datanode���յ�һ�����ݿ�Ķ���д������һ���߳�����ɣ�����Opendfs�Datanode�����һ������д�������漰������IO�ʹ���IO�����䵽��ͬ���̳߳��Эͬ��ɣ�ͨ���㿽��������sendfile�����ݿ齫�Ӵ���ֱ�ӿ��������緵�ظ�DFSClient�������û�̬���ں�̬�����ĵ��л����Ӷ�������ݵĴ���Ч�ʡ�
 * ��HDFS�У�DFSClient��Datanodeд���ݿ��ʱ�����ȰѴ�NamenodeҪ�ص�Datanode�б�����һ���ܵ����磺Datanode1 -> Datanode2 -> Datanode3�������ܵ��ﴮ�е�д���ݿ飬����Opendfs�У����ݿ齫���еĴ�DFSClient������Datanodeд��

# һ���򵥵��ļ�д���̣���ͼ2ʾ��
![ͼ2](https://github.com/liaosanity/Opendfs/images/writing_process.png)
                                     ͼ2
1) DFSClient����Namenode����д�ļ����󣬲��ṩ���ݿ��С�����踱������Ĭ��Ϊ3������Ϣ��
2) Namenode��������ĸ��������ؿ�д��Datanode�б�IPs�������ݿ�ֲ�����ʹ�÷��ص�IPs�ֲ��ڲ�ͬ�Ļ��ܣ���ÿ��IPֻ��һ�ݸ�����
3)DFSClient���ݷ��ص�IPs���е������Datanodeд���ݿ飻
4) Datanode1�յ����ݿ�д����д�뱾�ش��̣��ɹ�д��һ�������������Namenode�ϱ���
5) Datanode2�յ����ݿ�д����д�뱾�ش��̣��ɹ�д��һ�������������Namenode�ϱ���
6) Datanode3�յ����ݿ�д����д�뱾�ش��̣��ɹ�д��һ�������������Namenode�ϱ�����ΪDFSClient�ǲ��е�д���ݿ飬���Բ���4��5��6�����ϸ������ϵĴ��й�ϵ�����ǲ��еģ�
7) Datanode��Namenode�ϱ��յ�����ٸ�֪DFSClient���ݿ�ɹ�д�ꣻ
8) ����һ�����ݿ�����д�꣬�����Ҫд��һ�����ݿ飬���ظ�����1��ֱ���������ݿ�д�꣬����Namenode����ر��ļ�����

# һ���򵥵��ļ������̣���ͼ3ʾ��
![ͼ3](https://github.com/liaosanity/Opendfs/images/reading_process.png)
                                    ͼ3
1) DFSClient������һNamenode������ļ������ʵ�ǰҪ��ȡ���ļ����ݿ�ֲ�����Щ���ݽڵ��ϣ�
2) Namenode���ؿɶ���Datanode�б�IPs����ÿ�����ݿ鶼��������3������IP����һ�����󾡿��ܷ��ض�����ݿ��IP�б�Ĭ��Ϊ10���飩��
3) DFSClient���ݷ��ص�IPs������IP1��������ݿ��������ʧ�ܣ����IPs�б����޳����Ӷ���IP2��������ֱ�����ݿ�ɹ���ȡ��������б�������IP���������ʧ�ܣ�����Namenode�ϱ�Datanode�����ã�Ȼ���֪Ӧ�ò����ڿ�ȱʧ�������ļ���ȡʧ�ܣ�
4) ͬ����3���ζ�ȡ�ļ�����һ���飻
5) ͬ����3���ζ�ȡ�ļ�����һ���飬ֱ����ȡ�ļ������п顣

# һ�����ٵ��������ӣ�
## ��װ
  * ���������� 
    Linux��GCC4.8+
  * ���������
    yum -y install pcre-devel
  * Դ����룺
    ./configure --prefix=/home/opendfs
    make
    make install
## ����
  * �������ã���DFSClient��Namenode��Datanode������ͬһ̨�����ϣ���Namenode��Datanode��Ϊ���㣬����ɫ�������£�
```
#namenode.conf
Server server;
server.daemon = ALLOW;
server.workers = 8;
server.connections = 65536;
server.bind_for_cli = "0.0.0.0:8000";
server.bind_for_dn = "0.0.0.0:8001";
server.my_paxos = "0.0.0.0:8002";
server.ot_paxos = "0.0.0.0:8002";
server.paxos_group_num = 1;
server.checkpoint_num = 10000;
server.index_num = 1000000;
server.editlog_dir = "/data00/namenode/editlog";
server.fsimage_dir = "/data00/namenode/fsimage";
server.error_log = "/data00/namenode/logs/error.log";
server.pid_file = "/data00/namenode/pid/namenode.pid";
server.coredump_dir = "/data00/namenode/coredump";
server.log_level = LOG_INFO;
server.recv_buff_len = 64KB;
server.send_buff_len = 64KB;
server.max_tqueue_len = 1000;
server.dn_timeout = 600;

# datanode.conf
Server server;
server.daemon = ALLOW;
server.workers = 8;
server.connections = 65536;
server.bind_for_cli = "0.0.0.0:8100";
server.ns_srv = "127.0.0.1:8001";
server.data_dir = "/data01/block,/data02/block,/data03/block";
server.error_log = "/data00/datanode/logs/error.log";
server.pid_file = "/data00/datanode/pid/datanode.pid";
server.coredump_dir = "/data00/datanode/coredump/";
server.log_level = LOG_INFO;
server.recv_buff_len = 64KB;
server.send_buff_len = 64KB;
server.max_tqueue_len = 1000;
server.heartbeat_interval = 3;
server.block_report_interval = 3600;

# dfscli.conf
Server server;
server.daemon = ALLOW;
server.namenode_addr = "127.0.0.1:8000";
server.error_log = "";
server.log_level = LOG_INFO;
server.recv_buff_len = 64KB;
server.send_buff_len = 64KB;
server.blk_sz = 256MB;
server.blk_rep = 3;
``` 

 * ��Ⱥ���ã�����DFSClientһ̨��Namenode��Datanode��Ϊ3̨������ɫ�������£�
```
#namenode.conf
# namenode1
Server server;
server.daemon = ALLOW;
server.workers = 8;
server.connections = 65536;
server.bind_for_cli = "192.168.1.1:8000";
server.bind_for_dn = "192.168.1.1:8001";
server.my_paxos = "192.168.1.1:8002";
server.ot_paxos = "192.168.1.1:8002, 192.168.1.2:8002, 192.168.1.3:8002";
server.paxos_group_num = 1;
server.checkpoint_num = 10000;
server.index_num = 1000000;
server.editlog_dir = "/data00/namenode/editlog";
server.fsimage_dir = "/data00/namenode/fsimage";
server.error_log = "/data00/namenode/logs/error.log";
server.pid_file = "/data00/namenode/pid/namenode.pid";
server.coredump_dir = "/data00/namenode/coredump";
server.log_level = LOG_INFO;
server.recv_buff_len = 64KB;
server.send_buff_len = 64KB;
server.max_tqueue_len = 1000;
server.dn_timeout = 600;

# namenode2
Server server;
server.daemon = ALLOW;
server.workers = 8;
server.connections = 65536;
server.bind_for_cli = "192.168.1.2:8000";
server.bind_for_dn = "192.168.1.2:8001";
server.my_paxos = "192.168.1.2:8002";
server.ot_paxos = "192.168.1.1:8002, 192.168.1.2:8002, 192.168.1.3:8002";
server.paxos_group_num = 1;
server.checkpoint_num = 10000;
server.index_num = 1000000;
server.editlog_dir = "/data00/namenode/editlog";
server.fsimage_dir = "/data00/namenode/fsimage";
server.error_log = "/data00/namenode/logs/error.log";
server.pid_file = "/data00/namenode/pid/namenode.pid";
server.coredump_dir = "/data00/namenode/coredump";
server.log_level = LOG_INFO;
server.recv_buff_len = 64KB;
server.send_buff_len = 64KB;
server.max_tqueue_len = 1000;
server.dn_timeout = 600;

# namenode3
Server server;
server.daemon = ALLOW;
server.workers = 8;
server.connections = 65536;
server.bind_for_cli = "192.168.1.3:8000";
server.bind_for_dn = "192.168.1.3:8001";
server.my_paxos = "192.168.1.3:8002";
server.ot_paxos = "192.168.1.1:8002, 192.168.1.2:8002, 192.168.1.3:8002";
server.paxos_group_num = 1;
server.checkpoint_num = 10000;
server.index_num = 1000000;
# namenode.conf
# namenode1
Server server;
server.daemon = ALLOW;
server.workers = 8;
server.connections = 65536;
server.bind_for_cli = "192.168.1.1:8000";
server.bind_for_dn = "192.168.1.1:8001";
server.my_paxos = "192.168.1.1:8002";
server.ot_paxos = "192.168.1.1:8002, 192.168.1.2:8002, 192.168.1.3:8002";
server.paxos_group_num = 1;
server.checkpoint_num = 10000;
server.index_num = 1000000;
server.editlog_dir = "/data00/namenode/editlog";
server.fsimage_dir = "/data00/namenode/fsimage";
server.error_log = "/data00/namenode/logs/error.log";
server.pid_file = "/data00/namenode/pid/namenode.pid";
server.coredump_dir = "/data00/namenode/coredump";
server.log_level = LOG_INFO;
server.recv_buff_len = 64KB;
server.send_buff_len = 64KB;
server.max_tqueue_len = 1000;
server.dn_timeout = 600;

# namenode2
Server server;
server.daemon = ALLOW;
server.workers = 8;
server.connections = 65536;
server.bind_for_cli = "192.168.1.2:8000";
server.bind_for_dn = "192.168.1.2:8001";
server.my_paxos = "192.168.1.2:8002";
server.ot_paxos = "192.168.1.1:8002, 192.168.1.2:8002, 192.168.1.3:8002";
server.paxos_group_num = 1;
server.checkpoint_num = 10000;
server.index_num = 1000000;
server.editlog_dir = "/data00/namenode/editlog";
server.fsimage_dir = "/data00/namenode/fsimage";
server.error_log = "/data00/namenode/logs/error.log";
server.pid_file = "/data00/namenode/pid/namenode.pid";
server.coredump_dir = "/data00/namenode/coredump";
server.log_level = LOG_INFO;
server.recv_buff_len = 64KB;
server.send_buff_len = 64KB;
server.max_tqueue_len = 1000;
server.dn_timeout = 600;

# namenode3

# dfscli.conf
Server server;
server.daemon = ALLOW;
server.namenode_addr = "192.168.1.1:8000";
server.error_log = "";
server.log_level = LOG_INFO;
server.recv_buff_len = 64KB;
server.send_buff_len = 64KB;
server.blk_sz = 256MB;
server.blk_rep = 3;
```
