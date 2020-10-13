---
title: Configurar a FCI RHEL no SQL Server em Linux
description: Saiba como configurar uma FCI (instância de cluster de failover) de disco compartilhado RHEL (Red Hat Enterprise Linux) para alta disponibilidade do SQL Server em Linux.
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: dcc0a8d3-9d25-4208-8507-a5e65d2a9a15
ms.openlocfilehash: 617487d27842a6eb2c8844ae6c7ed2aa4e8fadce
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785078"
---
# <a name="configure-rhel-failover-cluster-instance-fci-cluster-for-sql-server"></a>Configurar o cluster de FCI (instância de cluster de failover) RHEL do SQL Server

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Este guia fornece instruções para criar um cluster de failover de disco compartilhado de dois nós para o SQL Server no Red Hat Enterprise Linux. A camada de clustering baseia-se no [complemento de HA](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) do RHEL (Red Hat Enterprise Linux) criado com base no [Pacemaker](https://clusterlabs.org/). A Instância do SQL Server está ativa em um nó ou no outro.

> [!NOTE] 
> O acesso ao complemento de HA do Red Hat e à documentação exige uma assinatura. 

Como mostra o diagrama a seguir, o armazenamento é apresentado a dois servidores. Os componentes de clustering – Corosync e Pacemaker – coordenam a comunicação e o gerenciamento de recursos. Um dos servidores tem a conexão ativa com os recursos de armazenamento e o SQL Server. Quando o Pacemaker detecta uma falha, os componentes de clustering gerenciam a movimentação dos recursos para o outro nó.  

![Cluster SQL de disco compartilhado do Red Hat Enterprise Linux 7](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

Para saber mais sobre configuração de cluster, opções de agentes de recursos e gerenciamento, acesse a [Documentação de referência do RHEL](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).


> [!NOTE] 
> Neste ponto, a integração do SQL Server com o Pacemaker não está tão acoplada quanto a do WSFC em Windows. No SQL, não há nenhum conhecimento sobre a presença do cluster, toda a orquestração ocorre de fora para dentro e o serviço é controlado como uma instância autônoma pelo Pacemaker. Além disso, por exemplo, as DMVs de cluster sys.dm_os_cluster_nodes e sys.dm_os_cluster_properties não terão registros.
Para usar uma cadeia de conexão que aponta para um nome do servidor de cadeia de caracteres e não usar o IP, elas precisarão se registrar no servidor DNS o IP usado para criar o recurso de IP virtual (conforme explicado nas seções a seguir) com o nome do servidor escolhido.

As seções a seguir descrevem as etapas necessárias para configurar uma solução de cluster de failover. 

## <a name="prerequisites"></a>Pré-requisitos

Para concluir o cenário de ponta a ponta a seguir, você precisará de dois computadores para implantar o cluster de dois nós e outro servidor para configurar o servidor NFS. As etapas abaixo descrevem como esses servidores serão configurados.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Instalar e configurar o sistema operacional em cada nó de cluster

A primeira etapa é configurar o sistema operacional nos nós de cluster. Para esse passo a passo, use o RHEL com uma assinatura válida para o complemento de HA. 

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>Instalar e configurar o SQL Server em cada nó de cluster

1. Instalar e configurar o SQL Server em ambos os nós.  Para obter instruções detalhadas, confira [Instalar o SQL Server em Linux](sql-server-linux-setup.md).

1. Designe um nó como primário e o outro como secundário para fins de configuração. Use esses termos para seguir este guia.  

1. No nó secundário, interrompa e desabilite o SQL Server.

   O seguinte exemplo interrompe e desabilita o SQL Server: 

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl disable mssql-server
   ```
> [!NOTE] 
> No momento da instalação, uma Chave Mestra do Servidor é gerada para a Instância do SQL Server e colocada em `/var/opt/mssql/secrets/machine-key`. No Linux, o SQL Server sempre é executado como uma conta local chamada mssql. Como é uma conta local, a identidade dela não é compartilhada entre os nós. Portanto, você precisa copiar a chave de criptografia do nó primário para cada nó secundário, de modo que cada conta mssql local possa acessá-la para descriptografar a Chave Mestra do Servidor. 

1. No nó primário, crie um logon do SQL Server para o Pacemaker e conceda a permissão de logon para executar `sp_server_diagnostics`. O Pacemaker usa essa conta para verificar qual nó está executando o SQL Server. 

   ```bash
   sudo systemctl start mssql-server
   ```

   Conecte-se ao banco de dados `master` do SQL Server com a conta SA e execute o seguinte:

   ```bashsql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'

   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```
   Alternativamente, você pode definir as permissões em um nível mais granular. O logon do Pacemaker exige que `VIEW SERVER STATE` consulte o status de integridade com sp_server_diagnostics e que `setupadmin` e `ALTER ANY LINKED SERVER` atualizem o nome da instância de FCI com o nome do recurso executando sp_dropserver e sp_addserver. 

1. No nó primário, interrompa e desabilite o SQL Server. 

1. Configure o arquivo de hosts para cada nó de cluster. O arquivo de host precisa incluir o endereço IP e o nome de cada nó de cluster. 

    Verifique o endereço IP de cada nó. O script a seguir mostra o endereço IP do nó atual. 

   ```bash
   sudo ip addr show
   ```

   Defina o nome do computador em cada nó. Dê a cada nó um nome exclusivo que tenha 15 caracteres ou menos. Defina o nome do computador adicionando-o a `/etc/hosts`. O script a seguir permite que você edite `/etc/hosts` com `vi`. 

   ```bash
   sudo vi /etc/hosts
   ```
   O exemplo a seguir mostra `/etc/hosts` com adições para dois nós chamados `sqlfcivm1` e `sqlfcivm2`.

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

Na próxima seção, você configurará o armazenamento compartilhado e moverá os arquivos de banco de dados para esse armazenamento. 

## <a name="configure-shared-storage-and-move-database-files"></a>Configurar o armazenamento compartilhado e mover arquivos de banco de dados 

Há uma variedade de soluções para fornecer armazenamento compartilhado. Este passo a passo demonstra como configurar o armazenamento compartilhado com o NFS. Recomendamos seguir as melhores práticas e usar o Kerberos para proteger o NFS (encontre um exemplo aqui: https://www.certdepot.net/rhel7-use-kerberos-control-access-nfs-network-shares/). 

>[!Warning]
>Se você não proteger o NFS, qualquer pessoa que possa acessar sua rede e falsificar o endereço IP de um nó SQL poderá acessar seus arquivos de dados. Como sempre, verifique se você tem o modelo de risco do sistema antes de usá-lo em produção. Outra opção de armazenamento é usar o compartilhamento de arquivo SMB.

### <a name="configure-shared-storage-with-nfs"></a>Configurar o armazenamento compartilhado com o NFS

> [!IMPORTANT] 
> Não há suporte para a hospedagem de arquivos de banco de dados em um servidor NFS com a versão <4 nesta versão. Isso inclui o uso do NFS para o clustering de failover de disco compartilhado, bem como bancos de dados em instâncias não clusterizadas. Estamos trabalhando para habilitar outras versões do servidor NFS nas versões futuras. 

No servidor NFS, faça o seguinte:

1. Instalar `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. Habilite e inicie o `rpcbind`

   ```bash
   sudo systemctl enable rpcbind && sudo systemctl start rpcbind
   ```

1. Habilite e inicie o `nfs-server`
 
   ```bash
   sudo systemctl enable nfs-server && sudo systemctl start nfs-server
   ```
 
1.  Edite `/etc/exports` para exportar o diretório que você deseja compartilhar. Você precisa de uma linha para cada compartilhamento desejado. Por exemplo: 

   ```bash
   /mnt/nfs  10.8.8.0/24(rw,sync,no_subtree_check,no_root_squash)
   ```

1. Exportar os compartilhamentos

   ```bash
   sudo exportfs -rav
   ```

1. Verifique se os caminhos são compartilhados/exportados e execute-os por meio do servidor NFS

   ```bash
   sudo showmount -e
   ```

1. Adicionar uma exceção no SELinux

   ```bash
   sudo setsebool -P nfs_export_all_rw 1
   ```
   
1. Abra o firewall do servidor.

   ```bash 
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>Configurar todos os nós de cluster para se conectar ao armazenamento compartilhado do NFS

Execute as etapas a seguir em todos os nós de cluster.

1.  Instalar `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. Abra o firewall em clientes e no servidor NFS

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

1. Verifique se você pode ver os compartilhamentos NFS nos computadores cliente

   ```bash
   sudo showmount -e <IP OF NFS SERVER>
   ```

1. Repita essas etapas em todos os nós de cluster.

Para obter mais informações sobre como usar o NFS, confira os seguintes recursos:

* [Servidores NFS e firewall | Stack Exchange](https://unix.stackexchange.com/questions/243756/nfs-servers-and-firewalld)
* [Como montar um volume do NFS | Guia de Administradores de Rede do Linux](https://www.tldp.org/LDP/nag2/x-087-2-nfs.mountd.html)
* [Configuração do servidor NFS | Portal do Cliente do Red Hat](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/storage_administration_guide/nfs-serverconfig)

### <a name="mount-database-files-directory-to-point-to-the-shared-storage"></a>Montar o diretório de arquivos de banco de dados para que ele aponte para o armazenamento compartilhado

1.  **Somente no nó primário**, salve os arquivos de banco de dados em uma localização temporária. O script a seguir, cria um diretório temporário, copia os arquivos de banco de dados para o novo diretório e remove os arquivos de banco de dados antigos. Enquanto o SQL Server é executado como o usuário local mssql, você precisa verificar se, após a transferência de dados para o compartilhamento montado, o usuário local tem acesso de leitura/gravação ao compartilhamento. 

   ``` 
   $ sudo su mssql
   $ mkdir /var/opt/mssql/tmp
   $ cp /var/opt/mssql/data/* /var/opt/mssql/tmp
   $ rm /var/opt/mssql/data/*
   $ exit
   ``` 

1.  Em todos os nós de cluster, edite o arquivo `/etc/fstab` para incluir o comando mount.  

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr 
   ```
   
   O script a seguir mostra um exemplo da edição.  

   ``` 
   10.8.8.0:/mnt/nfs /var/opt/mssql/data nfs timeo=14,intr 
   ``` 
> [!NOTE] 
>Se estiver usando um recurso FS do sistema de arquivos, conforme recomendado aqui, não haverá necessidade de preservar o comando de montagem em /etc/fstab. O Pacemaker se encarregará de montar a pasta quando ele iniciar o recurso clusterizado do FS. Com a ajuda do isolamento, ele garantirá que o FS nunca seja montado duas vezes. 

1.  Execute o comando `mount -a` para o sistema atualizar os caminhos montados.  

1.  Copie o banco de dados e os arquivos de log que você salvou em `/var/opt/mssql/tmp` para o compartilhamento recém-montado `/var/opt/mssql/data`. Isso só precisa ser feito **no nó primário**. Conceda permissões de leitura/gravação ao usuário local 'mssql'.

   ``` 
   $ sudo chown mssql /var/opt/mssql/data
   $ sudo chgrp mssql /var/opt/mssql/data
   $ sudo su mssql
   $ cp /var/opt/mssql/tmp/* /var/opt/mssql/data/
   $ rm /var/opt/mssql/tmp/*
   $ exit
   ``` 
 
1.  Verifique se o SQL Server é iniciado com êxito com o novo caminho de arquivo. Faça isso em cada nó. Neste ponto, apenas um nó deve executar o SQL Server por vez. Eles não podem ser executados ao mesmo tempo, porque tentarão acessar os arquivos de dados simultaneamente (para evitar a inicialização acidental do SQL Server em ambos os nós, use um recurso de cluster do sistema de arquivos para garantir que o compartilhamento não seja montado duas vezes por nós diferentes). Os comandos a seguir iniciam o SQL Server, verificam o status e, em seguida, interrompem o SQL Server.
 
   ```bash
   sudo systemctl start mssql-server
   sudo systemctl status mssql-server
   sudo systemctl stop mssql-server
   ```
 
Neste ponto, ambas as instâncias do SQL Server são configuradas para serem executadas com os arquivos de banco de dados no armazenamento compartilhado. A próxima etapa é configurar o SQL Server para o Pacemaker. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalar e configurar o Pacemaker em cada nó de cluster


2. Em ambos os nós de cluster, crie um arquivo para armazenar o nome de usuário do SQL Server e a senha para o logon do Pacemaker. O comando a seguir cria e popula este arquivo:

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   echo '<loginName>' | sudo tee -a /var/opt/mssql/secrets/passwd
   echo '<loginPassword>' | sudo tee -a /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd 
   sudo chmod 600 /var/opt/mssql/secrets/passwd    
   ```

3. Em ambos os nós de cluster, abra as portas de firewall do Pacemaker. Para abrir essas portas com o `firewalld`, execute o seguinte comando:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > Se você estiver usando outro firewall que não tenha uma configuração de alta disponibilidade interna, as portas a seguir precisarão ser abertas para que o Pacemaker possa se comunicar com outros nós no cluster
   >
   > * TCP: Portas 2224, 3121 e 21064
   > * UDP: Porta 5405

1. Instale os pacotes do Pacemaker em cada nó.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

    

2. Defina a senha do usuário padrão criado ao instalar pacotes do Pacemaker e do Corosync. Use a mesma senha em ambos os nós. 

   ```bash
   sudo passwd hacluster
   ```

    

3. Habilite e inicie o serviço `pcsd` e o Pacemaker. Isso permitirá que os nós reingressem no cluster após a reinicialização. Execute o comando a seguir em ambos os nós.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Instalar o agente do recurso FCI para SQL Server. Execute os comandos a seguir em ambos os nós. 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="configure-fencing-agent"></a>Configurar um agente de isolamento

Um dispositivo STONITH fornece um agente de isolamento. [Como configurar o Pacemaker no Red Hat Enterprise Linux no Azure](/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-pacemaker/#1-create-the-stonith-devices) fornece um exemplo de como criar um dispositivo STONITH para esse cluster no Azure. Modifique as instruções de seu ambiente.

## <a name="create-the-cluster"></a>Criar o cluster 

1. Em um dos nós, crie o cluster.

   ```bash
   sudo pcs cluster auth <nodeName1 nodeName2 ...> -u hacluster
   sudo pcs cluster setup --name <clusterName> <nodeName1 nodeName2 ...>
   sudo pcs cluster start --all
   ```

2. Configure os recursos de cluster para o SQL Server, o sistema de arquivos e os recursos de IP virtual e envie a configuração por push para o cluster. Você precisará das seguintes informações:

   - **Nome do Recurso do SQL Server**: Um nome para o recurso clusterizado do SQL Server. 
   - **Nome do Recurso de IP Flutuante**: Um nome para o recurso de endereço IP virtual.
   - **Endereço IP**: O endereço IP que os clientes usarão para se conectarem à instância clusterizada do SQL Server. 
   - **Nome do Recurso do Sistema de Arquivos**: Um nome para o recurso do sistema de arquivos.
   - **dispositivo**: O caminho do compartilhamento NFS
   - **dispositivo**: O caminho local que está montado no compartilhamento
   - **fstype**: Tipo de compartilhamento de arquivo (ou seja, NFS)

   Atualize os valores com base no script a seguir para o seu ambiente. Faça a execução em um nó para configurar e iniciar o serviço clusterizado.  

   ```bash
   sudo pcs cluster cib cfg 
   sudo pcs -f cfg resource create <sqlServerResourceName> ocf:mssql:fci
   sudo pcs -f cfg resource create <floatingIPResourceName> ocf:heartbeat:IPaddr2 ip=<ip Address>
   sudo pcs -f cfg resource create <fileShareResourceName> Filesystem device=<networkPath> directory=<localPath>         fstype=<fileShareType>
   sudo pcs -f cfg constraint colocation add <virtualIPResourceName> <sqlResourceName>
   sudo pcs -f cfg constraint colocation add <fileShareResourceName> <sqlResourceName> 
   sudo pcs cluster cib-push cfg
   ```

   Por exemplo, o script a seguir cria um recurso clusterizado do SQL Server chamado `mssqlha` e um recurso de IP flutuante com o endereço IP `10.0.0.99`. Ele também cria um recurso do sistema de arquivos e adiciona restrições para que todos os recursos sejam colocados no mesmo nó do recurso do SQL. 

   ```bash
   sudo pcs cluster cib cfg
   sudo pcs -f cfg resource create mssqlha ocf:mssql:fci
   sudo pcs -f cfg resource create virtualip ocf:heartbeat:IPaddr2 ip=10.0.0.99
   sudo pcs -f cfg resource create fs Filesystem device="10.8.8.0:/mnt/nfs" directory="/var/opt/mssql/data" fstype="nfs"
   sudo pcs -f cfg constraint colocation add virtualip mssqlha
   sudo pcs -f cfg constraint colocation add fs mssqlha
   sudo pcs cluster cib-push cfg
   ```

   Depois que a configuração for enviada por push, o SQL Server será iniciado em um nó. 

3. Verifique se o SQL Server foi iniciado. 

   ```bash
   sudo pcs status 
   ```

   Os exemplos a seguir mostram os resultados de quando o Pacemaker iniciou com êxito uma instância clusterizada do SQL Server. 

   ```
   fs     (ocf::heartbeat:Filesystem):    Started sqlfcivm1
   virtualip     (ocf::heartbeat:IPaddr2):      Started sqlfcivm1
   mssqlha  (ocf::mssql:fci): Started sqlfcivm1
   
   PCSD Status:
    sqlfcivm1: Online
    sqlfcivm2: Online
   
   Daemon Status:
    corosync: active/disabled
    pacemaker: active/enabled
    pcsd: active/enabled
   ```

## <a name="additional-resources"></a>Recursos adicionais

* Guia [Cluster do zero](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf) do Pacemaker

## <a name="next-steps"></a>Próximas etapas

[Operar o SQL Server em um cluster de disco compartilhado do Red Hat Enterprise Linux](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
