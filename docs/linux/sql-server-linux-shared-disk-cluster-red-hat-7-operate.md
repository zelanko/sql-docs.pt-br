---
title: Operar a FCI RHEL do SQL Server em Linux
description: Saiba como operar uma FCI (instância de cluster de failover) de disco compartilhado RHEL (Red Hat Enterprise Linux) do SQL Server para alta disponibilidade, como fazer failover manual da FCI e adicionar nós ao cluster ou removê-los do cluster.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 075ab7d8-8b68-43f3-9303-bbdf00b54db1
ms.openlocfilehash: 76c59c6c7b821bfcc9eb76ca3a694a1c69095ce1
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558521"
---
# <a name="operate-rhel-failover-cluster-instance-fci-for-sql-server"></a>Operar a FCI (instância de cluster de failover) RHEL do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento descreve como executar as tarefas a seguir para o SQL Server em um cluster de failover de disco compartilhado com o Red Hat Enterprise Linux.

- Fazer failover do cluster manualmente
- Monitorar um serviço SQL Server de cluster de failover
- Adicionar um nó de cluster
- Remover um nó de cluster
- Alterar a frequência de monitoramento de recursos do SQL Server

## <a name="architecture-description"></a>Descrição da arquitetura

A camada de clustering baseia-se no [complemento de HA](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) do RHEL (Red Hat Enterprise Linux) criado com base no [Pacemaker](https://clusterlabs.org/). O Corosync e o Pacemaker coordenam a comunicação de cluster e o gerenciamento de recursos. A Instância do SQL Server está ativa em um nó ou no outro.

O diagrama a seguir ilustra os componentes em um cluster do Linux com o SQL Server. 

![Cluster SQL de disco compartilhado do Red Hat Enterprise Linux 7](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

Para saber mais sobre configuração de cluster, opções de agentes de recursos e gerenciamento, acesse a [Documentação de referência do RHEL](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).

## <a name = "failManual"></a>Fazer failover do cluster manualmente

O comando `resource move` cria uma restrição que força o recurso a ser reiniciado no nó de destino.  Depois de executar o comando `move`, a execução do recurso `clear` removerá a restrição, de modo que seja possível mover o recurso novamente ou fazer o failover do recurso automaticamente. 

```bash
sudo pcs resource move <sqlResourceName> <targetNodeName>  
sudo pcs resource clear <sqlResourceName> 
```

O exemplo a seguir move o recurso **mssqlha** para um nó chamado **sqlfcivm2** e, em seguida, remove a restrição, de modo que o recurso possa ser movido para outro nó posteriormente.  

```bash
sudo pcs resource move mssqlha sqlfcivm2 
sudo pcs resource clear mssqlha 
```

## <a name="monitor-a-failover-cluster-sql-server-service"></a>Monitorar um serviço SQL Server de cluster de failover

Exiba o status atual do cluster:

```bash
sudo pcs status  
```

Exiba o status ativo de cluster e recursos:

```bash
sudo crm_mon 
```

Exiba os logs do agente de recursos em `/var/log/cluster/corosync.log`

## <a name="add-a-node-to-a-cluster"></a>Adicionar um nó a um cluster

1. Verifique o endereço IP de cada nó. O script a seguir mostra o endereço IP do nó atual. 

   ```bash
   ip addr show
   ```

3. O novo nó precisa de um nome exclusivo que tenha 15 caracteres ou menos. Por padrão, no Red Hat Linux, o nome do computador é `localhost.localdomain`. Esse nome padrão pode não ser exclusivo e é muito longo. Defina o nome do computador como o novo nó. Defina o nome do computador adicionando-o a `/etc/hosts`. O script a seguir permite que você edite `/etc/hosts` com `vi`. 

   ```bash
   sudo vi /etc/hosts
   ```

   O exemplo a seguir mostra `/etc/hosts` com adições para três nós chamados `sqlfcivm1`, `sqlfcivm2` e `sqlfcivm3`.

   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1         localhost localhost6 localhost6.localdomain6
   10.128.18.128 fcivm1
   10.128.16.77 fcivm2
   10.128.14.26 fcivm3
    ```
    
   O arquivo deve ser o mesmo em todos os nós. 

1. Interrompa o serviço SQL Server no novo nó.

1. Siga as instruções para montar o diretório do arquivo de banco de dados na localização compartilhada:

   No servidor NFS, instale `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils 
   ``` 

   Abra o firewall em clientes e no servidor NFS 

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

   Edite o arquivo /etc/fstab para incluir o comando mount: 

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr
   ```

   Execute `mount -a` para que as alterações entrem em vigor.
   
1. No novo nó, crie um arquivo para armazenar o nome de usuário e a senha do SQL Server para o logon do Pacemaker. O comando a seguir cria e popula este arquivo:

   ```bash
   sudo touch /var/opt/mssql/passwd
   sudo echo "<loginName>" >> /var/opt/mssql/secrets/passwd
   sudo echo "<loginPassword>" >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/passwd
   sudo chmod 600 /var/opt/mssql/passwd
   ```

3. No novo nó, abra as portas do firewall do Pacemaker. Para abrir essas portas com o `firewalld`, execute o seguinte comando:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > [!NOTE]
   > Se você estiver usando outro firewall que não tenha uma configuração de alta disponibilidade interna, as portas a seguir precisarão ser abertas para que o Pacemaker possa se comunicar com outros nós no cluster
   >
   > * TCP: Portas 2224, 3121 e 21064
   > * UDP: Porta 5405

1. Instale os pacotes do Pacemaker no novo nó.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```
 
2. Defina a senha do usuário padrão criado ao instalar pacotes do Pacemaker e do Corosync. Use a mesma senha dos nós existentes. 

   ```bash
   sudo passwd hacluster
   ```
 
3. Habilite e inicie o serviço `pcsd` e o Pacemaker. Isso permitirá que o novo nó reingresse no cluster após a reinicialização. Execute o comando a seguir no novo nó.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Instalar o agente do recurso FCI para SQL Server. Execute os comandos a seguir no novo nó. 

   ```bash
   sudo yum install mssql-server-ha
   ```

1. Em um nó existente do cluster, autentique o novo nó e adicione-o ao cluster:

    ```bash
    sudo pcs    cluster auth <nodeName3> -u hacluster 
    sudo pcs    cluster node add <nodeName3> 
    ```

    O exemplo a seguir adiciona um nó chamado **vm3** ao cluster.

    ```bash
    sudo pcs    cluster auth  
    sudo pcs    cluster start 
    ```

## <a name="remove-nodes-from-a-cluster"></a>Remover nós de um cluster

Para remover um nó de um cluster, execute o seguinte comando:

```bash
sudo pcs    cluster node remove <nodeName>  
```

## <a name="change-the-frequency-of-sqlservr-resource-monitoring-interval"></a>Alterar a frequência do intervalo de monitoramento do recurso sqlservr

```bash
sudo pcs    resource op monitor interval=<interval>s <sqlResourceName> 
```

O seguinte exemplo define o intervalo de monitoramento como 2 segundos para o recurso mssql:

```bash
sudo pcs    resource op monitor interval=2s mssqlha 
```
## <a name="troubleshoot-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Solução de problemas do cluster de disco compartilhado do Red Hat Enterprise Linux para o SQL Server

Na solução de problemas do cluster, talvez seja útil entender como os três daemons funcionam em conjunto para gerenciar os recursos de cluster. 

| Daemon | Descrição 
| ----- | -----
| Corosync | Fornece associação de quorum e mensagens entre os nós de cluster.
| Pacemaker | Reside na parte superior do Corosync e fornece computadores de estado para recursos. 
| PCSD | Gerencia o Pacemaker e o Corosync por meio das ferramentas `pcs`

O PCSD precisa estar em execução para que as ferramentas `pcs` sejam usadas. 

### <a name="current-cluster-status"></a>Status atual do cluster 

`sudo pcs status` retorna informações básicas sobre o cluster, o quorum, os nós, os recursos e o status do daemon de cada nó. 

Um exemplo de uma saída de quorum íntegra do Pacemaker é:

```
Cluster name: MyAppSQL 
Last updated: Wed Oct 31 12:00:00 2016  Last change: Wed Oct 31 11:00:00 2016 by root via crm_resource on sqlvmnode1 
Stack: corosync 
Current DC: sqlvmnode1  (version 1.1.13-10.el7_2.4-44eb2dd) - partition with quorum 
3 nodes and 1 resource configured 

Online: [ sqlvmnode1 sqlvmnode2 sqlvmnode3] 

Full list of resources: 

mssqlha (ocf::sql:fci): Started sqlvmnode1 

PCSD Status: 
sqlvmnode1: Online 
sqlvmnode2: Online 
sqlvmnode3: Online 

Daemon Status: 
corosync: active/disabled 
pacemaker: active/enabled 
```

No exemplo, `partition with quorum` significa que um quorum de maioria dos nós está online. Se o cluster perder um quorum de maioria dos nós, `pcs status` retornará `partition WITHOUT quorum` e todos os recursos serão interrompidos. 

`online: [sqlvmnode1 sqlvmnode2 sqlvmnode3]` retorna o nome de todos os nós que participam atualmente do cluster. Se algum nó não estiver participando, `pcs status` retornará `OFFLINE: [<nodename>]`.

`PCSD Status` mostra o status do cluster de cada nó.

### <a name="reasons-why-a-node-may-be-offline"></a>Motivos pelos quais um nó pode estar offline

Verifique os itens a seguir quando um nó estiver offline.

- **Firewall**

    As portas a seguir precisam ser abertas em todos os nós para que o Pacemaker possa se comunicar.
    
    - **TCP: 2224, 3121 e 21064

- **Serviços do Pacemaker ou do Corosync em execução**

- **Comunicação dos nós**

- **Mapeamentos de nomes de nós**

## <a name="additional-resources"></a>Recursos adicionais

* Guia [Cluster do zero](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf) do Pacemaker

## <a name="next-steps"></a>Próximas etapas

[Configurar o cluster de disco compartilhado do Red Hat Enterprise Linux para o SQL Server](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)

