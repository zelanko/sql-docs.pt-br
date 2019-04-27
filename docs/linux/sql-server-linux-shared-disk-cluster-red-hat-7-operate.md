---
title: Operar o cluster compartilhado do Red Hat Enterprise Linux para SQL Server | Microsoft Docs
description: Implementar a alta disponibilidade por meio da configuração de cluster de disco compartilhado do Red Hat Enterprise Linux para o SQL Server.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 075ab7d8-8b68-43f3-9303-bbdf00b54db1
ms.openlocfilehash: 2967277ca109b9ee55221a7b12f5af891a5e45a2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62635582"
---
# <a name="operate-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Operar o cluster de disco compartilhado do Red Hat Enterprise Linux para SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento descreve como realizar as seguintes tarefas para o SQL Server em um cluster de failover de disco compartilhado com Red Hat Enterprise Linux.

- Faça failover manualmente o cluster
- Monitorar um cluster de failover do serviço do SQL Server
- Adicionar um nó de cluster
- Remover um nó de cluster
- Alterar a frequência de monitoramento de recurso do SQL Server

## <a name="architecture-description"></a>Descrição de arquitetura

A camada de clustering é baseada no Red Hat Enterprise Linux (RHEL) [complemento HA](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) criado na parte superior da [Pacemaker](https://clusterlabs.org/). Corosync e Pacemaker coordenam as comunicações de cluster e gerenciamento de recursos. Instância do SQL Server está ativa em um nó ou em outro.

O diagrama a seguir ilustra os componentes em um cluster do Linux com o SQL Server. 

![Red Hat Enterprise Linux 7 compartilhado de Cluster de disco do SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

Para obter mais informações sobre a configuração de cluster, opções de agentes de recursos e gerenciamento, visite [documentação de referência do RHEL](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).

## <a name = "failManual"></a>Cluster de failover manualmente

O `resource move` comando cria uma restrição de forçar o recurso para iniciar no nó de destino.  Depois de executar o `move` comando, executando recursos `clear` removerá a restrição, portanto, é possível mover o recurso novamente ou fazer com que o recurso de failover automaticamente. 

```bash
sudo pcs resource move <sqlResourceName> <targetNodeName>  
sudo pcs resource clear <sqlResourceName> 
```

O exemplo a seguir move o **mssqlha** recursos para um nó chamado **sqlfcivm2**e, em seguida, remove a restrição para que o recurso possa mover para um nó diferente mais tarde.  

```bash
sudo pcs resource move mssqlha sqlfcivm2 
sudo pcs resource clear mssqlha 
```

## <a name="monitor-a-failover-cluster-sql-server-service"></a>Monitorar um cluster de failover do serviço do SQL Server

Exiba o status atual do cluster:

```bash
sudo pcs status  
```

Exibir o status em tempo real do cluster e recursos:

```bash
sudo crm_mon 
```

Exibir os logs de agente de recursos no `/var/log/cluster/corosync.log`

## <a name="add-a-node-to-a-cluster"></a>Adicionar um nó a um cluster

1. Verifique o endereço IP para cada nó. O script a seguir mostra o endereço IP do nó atual. 

   ```bash
   ip addr show
   ```

3. O novo nó precisa de um nome exclusivo que é de 15 caracteres ou menos. Por padrão no Red Hat Linux é o nome do computador `localhost.localdomain`. Esse nome padrão pode não ser exclusivo e é muito longo. Defina o nome do computador com o novo nó. Definir o nome do computador, adicionando-o para `/etc/hosts`. O script a seguir permite que você edite `/etc/hosts` com `vi`. 

   ```bash
   sudo vi /etc/hosts
   ```

   A exemplo a seguir mostra `/etc/hosts` com adições para três nós denominados `sqlfcivm1`, `sqlfcivm2`, e`sqlfcivm3`.

   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1         localhost localhost6 localhost6.localdomain6
   10.128.18.128 fcivm1
   10.128.16.77 fcivm2
   10.128.14.26 fcivm3
    ```
    
   O arquivo deve ser o mesmo em todos os nós. 

1. Interrompa o serviço do SQL Server no novo nó.

1. Siga as instruções para montar o diretório de arquivos de banco de dados para o local compartilhado:

   Do servidor NFS, instalar `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils 
   ``` 

   Abra o firewall em clientes e servidor NFS 

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

   Edite o arquivo /etc/fstab para incluir o comando de montagem: 

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr
   ```

   Execute `mount -a` para que as alterações entrem em vigor.
   
1. No novo nó, crie um arquivo para armazenar o nome de usuário do SQL Server e a senha para o logon do Pacemaker. O comando a seguir cria e popula este arquivo:

   ```bash
   sudo touch /var/opt/mssql/passwd
   sudo echo "<loginName>" >> /var/opt/mssql/secrets/passwd
   sudo echo "<loginPassword>" >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/passwd
   sudo chmod 600 /var/opt/mssql/passwd
   ```

3. No novo nó, abra as portas de firewall do Pacemaker. Para abrir essas portas com o `firewalld`, execute o seguinte comando:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > [!NOTE]
   > Se você estiver usando outro firewall que não tem uma configuração de alta disponibilidade interna, as seguintes portas precisam ser abertas para o Pacemaker seja capaz de se comunicar com outros nós no cluster
   >
   > * TCP: Ports 2224, 3121, 21064
   > * UDP: Porta 5405

1. Instale os pacotes do Pacemaker no novo nó.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```
 
2. Defina a senha do usuário padrão criado ao instalar pacotes do Pacemaker e do Corosync. Use a mesma senha que os nós existentes. 

   ```bash
   sudo passwd hacluster
   ```
 
3. Habilite e inicie o serviço `pcsd` e o Pacemaker. Isso permitirá que o novo nó reingressar no cluster após a reinicialização. Execute o seguinte comando no novo nó.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Instalar o agente do recurso FCI para SQL Server. Execute os seguintes comandos no novo nó. 

   ```bash
   sudo yum install mssql-server-ha
   ```

1. Em um nó existente do cluster, autenticar o novo nó e adicioná-lo ao cluster:

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

Para remover um nó de um cluster que execute o seguinte comando:

```bash
sudo pcs    cluster node remove <nodeName>  
```

## <a name="change-the-frequency-of-sqlservr-resource-monitoring-interval"></a>Alterar a frequência do intervalo de monitoramento de recursos do sqlservr

```bash
sudo pcs    resource op monitor interval=<interval>s <sqlResourceName> 
```

O exemplo a seguir define o intervalo de monitoramento para 2 segundos para o recurso de mssql:

```bash
sudo pcs    resource op monitor interval=2s mssqlha 
```
## <a name="troubleshoot-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Solucionar problemas de cluster de disco compartilhado do Red Hat Enterprise Linux para SQL Server

Na solução de problemas do cluster, ele pode ajudar a entender como os três daemons funcionam juntos para gerenciar recursos de cluster. 

| Daemon | Descrição 
| ----- | -----
| Corosync | Fornece associação de quorum e mensagens entre nós de cluster.
| Pacemaker | Reside na parte superior do Corosync e fornece máquinas de estado para os recursos. 
| PCSD | Gerencia o Pacemaker e do Corosync por meio de `pcs` ferramentas

PCSD deve estar em execução para usar `pcs` ferramentas. 

### <a name="current-cluster-status"></a>Status atual do cluster 

`sudo pcs status` Retorna informações básicas sobre o status do cluster, quorum, nós, recursos e o daemon para cada nó. 

Um exemplo de uma saída de quorum Íntegro pacemaker seria:

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

No exemplo, `partition with quorum` significa que um quorum de maioria de nós está online. Se o cluster perder um quorum de maioria de nós, `pcs status` retornará `partition WITHOUT quorum` e todos os recursos serão interrompidos. 

`online: [sqlvmnode1 sqlvmnode2 sqlvmnode3]` Retorna o nome de todos os nós que estão participando do cluster. Se não estiverem participando de todos os nós, `pcs status` retorna `OFFLINE: [<nodename>]`.

`PCSD Status` mostra o status do cluster para cada nó.

### <a name="reasons-why-a-node-may-be-offline"></a>Motivos pelos quais um nó pode estar offline

Verifique os itens a seguir, quando um nó está offline.

- **Firewall**

    As seguintes portas precisam ser abertas em todos os nós para Pacemaker seja capaz de se comunicar.
    
    - **TCP: 2224, 3121, 21064

- **Pacemaker ou Corosync serviços em execução**

- **Comunicação de nó**

- **Mapeamentos de nome de nó**

## <a name="additional-resources"></a>Recursos adicionais

* [Desde o início do cluster](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf) guia do Pacemaker

## <a name="next-steps"></a>Próximas etapas

[Configurar o cluster de disco compartilhado do Red Hat Enterprise Linux para SQL Server](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)

