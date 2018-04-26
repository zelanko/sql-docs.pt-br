---
title: Configurar o cluster compartilhado do Red Hat Enterprise Linux para o SQL Server | Microsoft Docs
description: Implementar a alta disponibilidade por meio da configuração de cluster de disco compartilhado do Red Hat Enterprise Linux para o SQL Server.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: dcc0a8d3-9d25-4208-8507-a5e65d2a9a15
ms.workload: On Demand
ms.openlocfilehash: 69f0953d6a03231b86ba9fb7a13bbddea2a48a22
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="configure-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Configurar o cluster de disco compartilhado do Red Hat Enterprise Linux para o SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este guia fornece instruções para criar um cluster de disco compartilhado de dois nós para o SQL Server no Red Hat Enterprise Linux. A camada de clustering é baseada no Red Hat Enterprise Linux (RHEL) [HA complemento](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) criado na parte superior do [Pacemaker](http://clusterlabs.org/). Instância do SQL Server está ativa em um nó ou em outro.

> [!NOTE] 
> Acesso ao complemento Red Hat HA e documentação requer uma assinatura. 

Como mostra o diagrama a seguir, o armazenamento é apresentado a dois servidores. Componentes de clusters - Corosync e Pacemaker - coordenam a comunicação e gerenciamento de recursos. Um dos servidores tem a conexão ativa os recursos de armazenamento e o SQL Server. Quando Pacemaker detecta uma falha de componentes de clusters gerenciam mover os recursos para o outro nó.  

![Red Hat Enterprise Linux 7 compartilhado de Cluster de disco do SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

Para obter mais informações sobre a configuração de cluster recurso agentes e opções de gerenciamento, visite [documentação de referência do RHEL](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).


> [!NOTE] 
> Neste ponto, a integração do SQL Server com Pacemaker não é como acoplada como com o WSFC no Windows. De dentro do SQL, não há nenhum conhecimento sobre a presença do cluster, orquestração todas as está fora de e o serviço é controlado como uma instância autônoma por Pacemaker. Também, por exemplo, dm_os_cluster_properties e sys.DM os_cluster_nodes dmvs de cluster não serão nenhum registro.
Para usar uma cadeia de caracteres de conexão que aponta para um nome de servidor de cadeia de caracteres e não usar o IP, será necessário registrar o IP usado para criar o recurso IP virtual (conforme explicado nas seções a seguir) no seu servidor DNS com o nome de servidor escolhido.

As seções a seguir percorrer as etapas para configurar uma solução de cluster de failover. 

## <a name="prerequisites"></a>Prerequisites

Para concluir o seguinte cenário de ponta a ponta, você precisa de duas máquinas para implantar o cluster de dois nós e outro servidor para configurar o servidor NFS. Etapas a seguir descrevem como esses servidores serão configurados.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Instalar e configurar o sistema operacional em cada nó de cluster

A primeira etapa é configurar o sistema operacional em nós de cluster. Para este passo a passo, use RHEL com uma assinatura válida para o complemento de alta disponibilidade. 

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>Instalar e configurar o SQL Server em cada nó de cluster

1. Instalar e configurar o SQL Server em ambos os nós.  Para obter instruções detalhadas, consulte [instalar o SQL Server no Linux](sql-server-linux-setup.md).

1. Designe um nó como primário e o outro como secundário, para fins de configuração. Usar essas condições para o seguinte neste guia.  

1. No nó secundário, interromper e desabilitar o SQL Server.

   O exemplo a seguir para e desabilita o SQL Server: 

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl disable mssql-server
   ```
> [!NOTE] 
> No momento da instalação, uma chave mestre do servidor é gerado para a instância do SQL Server e colocado no `/var/opt/mssql/secrets/machine-key`. No Linux, o SQL Server sempre é executado como uma conta local chamada mssql. Como é uma conta local, sua identidade não é compartilhada entre nós. Portanto, é necessário copiar a chave de criptografia do nó principal para cada nó secundário para que cada conta mssql local pode acessá-lo para descriptografar a chave mestra do servidor. 

1. No nó primário, crie um logon do SQL server para Pacemaker e conceder a permissão de logon para executar `sp_server_diagnostics`. Pacemaker usa essa conta para verificar qual nó está executando o SQL Server. 

   ```bash
   sudo systemctl start mssql-server
   ```

   Conecte-se ao SQL Server `master` de banco de dados com a conta sa e execute o seguinte:

   ```bashsql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'

   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```
   Alternativamente, você pode definir as permissões em um nível mais granular. Requer o logon de Pacemaker `VIEW SERVER STATE` para consultar o status de integridade com sp_server_diagnostics, `setupadmin` e `ALTER ANY LINKED SERVER` para atualizar o nome da instância FCI com o nome do recurso executando sp_dropserver e sp_addserver. 

1. No nó primário, interrompa e desabilite o SQL Server. 

1. Configure o arquivo de hosts para cada nó do cluster. O arquivo de host deve incluir o endereço IP e o nome de cada nó de cluster. 

    Verifique o endereço IP para cada nó. O script a seguir mostra o endereço IP do nó atual. 

   ```bash
   sudo ip addr show
   ```

   Defina o nome do computador em cada nó. Dê a cada nó de um nome exclusivo que é de 15 caracteres ou menos. Definir o nome do computador, adicionando-o para `/etc/hosts`. O script a seguir permite que você edite `/etc/hosts` com `vi`. 

   ```bash
   sudo vi /etc/hosts
   ```
   A exemplo a seguir mostra `/etc/hosts` com adições de dois nós denominados `sqlfcivm1` e `sqlfcivm2`.

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

Na próxima seção, você irá configurar o armazenamento compartilhado e mover os arquivos de banco de dados para que o armazenamento. 

## <a name="configure-shared-storage-and-move-database-files"></a>Configurar o armazenamento compartilhado e mover arquivos de banco de dados 

Há uma variedade de soluções para fornecer armazenamento compartilhado. Este passo a passo demonstra como configurar o armazenamento compartilhado com NFS. Recomendamos que siga as práticas recomendadas e usar o Kerberos para proteger NFS (você pode encontrar um exemplo aqui: https://www.certdepot.net/rhel7-use-kerberos-control-access-nfs-network-shares/). 

>[!Warning]
>Se você não proteger NFS, quem pode acessar sua rede e falsificar o endereço IP de um nó do SQL será capaz de acessar os arquivos de dados. Como sempre, certifique-se de seu sistema de modelo de ameaça você antes de usá-lo em produção. Outra opção de armazenamento é usar o compartilhamento de arquivos SMB.

### <a name="configure-shared-storage-with-nfs"></a>Configurar o armazenamento compartilhado com NFS

> [!IMPORTANT] 
> Arquivos de banco de dados em um servidor NFS com versão de hospedagem < 4 não tem suporte nesta versão. Isso inclui usar o NFS disco compartilhado para clustering de failover, bem como bancos de dados em instâncias não clusterizado. Estamos trabalhando para habilitar outras versões do servidor NFS nas versões futuras. 

No servidor NFS, faça o seguinte:

1. Instalar o `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. Habilitar e iniciar `rpcbind`

   ```bash
   sudo systemctl enable rpcbind && sudo systemctl start rpcbind
   ```

1. Habilitar e iniciar `nfs-server`
 
   ```bash
   sudo systemctl enable nfs-server && sudo systemctl start nfs-server
   ```
 
1.  Editar `/etc/exports` para exportar o diretório que você deseja compartilhar. Você precisa de 1 linha para cada compartilhamento que você deseja. Por exemplo: 

   ```bash
   /mnt/nfs  10.8.8.0/24(rw,sync,no_subtree_check,no_root_squash)
   ```

1. Exportar os compartilhamentos

   ```bash
   sudo exportfs -rav
   ```

1. Verifique se os caminhos são compartilhados/exportado, executar do servidor NFS

   ```bash
   sudo showmount -e
   ```

1. Adicionar exceção em SELinux

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

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>Configurar todos os nós de cluster para se conectar ao armazenamento compartilhado NFS

Execute as seguintes etapas em todos os nós de cluster.

1.  Instalar o `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. Abra o firewall em clientes e servidor NFS

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

1. Verifique se que você pode ver os compartilhamentos NFS em computadores cliente

   ```bash
   sudo showmount -e <IP OF NFS SERVER>
   ```

1. Repita essas etapas em todos os nós de cluster.

Para obter mais informações sobre como usar o NFS, consulte os seguintes recursos:

* [NFS servidores e firewalld | Troca de pilha](http://unix.stackexchange.com/questions/243756/nfs-servers-and-firewalld)
* [Montar um Volume de NFS | Guia do administrador de rede do Linux](http://www.tldp.org/LDP/nag2/x-087-2-nfs.mountd.html)
* [Configuração do servidor NFS](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/3/html/Reference_Guide/s1-nfs-server-export.html)

### <a name="mount-database-files-directory-to-point-to-the-shared-storage"></a>Diretório de arquivos de banco de dados de montagem para apontar para o armazenamento compartilhado

1.  **No nó primário**, salvar os arquivos de banco de dados para um local temporário. O script a seguir, cria um novo diretório temporário, copia os arquivos de banco de dados para o novo diretório e remove os arquivos de banco de dados antigo. Como o SQL Server é executado como usuário local mssql, você precisa garantir que, após a transferência de dados para o compartilhamento montado, usuário local tenha acesso de leitura / gravação ao compartilhamento de. 

   ``` 
   $ sudo su mssql
   $ mkdir /var/opt/mssql/tmp
   $ cp /var/opt/mssql/data/* /var/opt/mssql/tmp
   $ rm /var/opt/mssql/data/*
   $ exit
   ``` 

1.  Em todos os nós de cluster editar `/etc/fstab` arquivo para incluir o comando de montagem.  

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr 
   ```
   
   O script a seguir mostra um exemplo da edição.  

   ``` 
   10.8.8.0:/mnt/nfs /var/opt/mssql/data nfs timeo=14,intr 
   ``` 
> [!NOTE] 
>Se usar um recurso do sistema de arquivos (FS) conforme recomendado aqui, não é necessário para preservar o comando de montagem no /etc/fstab. Pacemaker cuidará de montar a pasta quando ele inicia o recurso FS clusterizado. Com a Ajuda de isolamento, ele garantirá que o FS nunca é montado duas vezes. 

1.  Execute `mount -a` comando para o sistema atualizar os caminhos montados.  

1.  Copie os arquivos de log e banco de dados que você salvou `/var/opt/mssql/tmp` para o compartilhamento recentemente montado `/var/opt/mssql/data`. Isso só precisa ser feito **no nó primário**. Certifique-se de que você forneça permissões de leitura e gravação ao usuário local 'mssql'.

   ``` 
   $ sudo chown mssql /var/opt/mssql/data
   $ sudo chgrp mssql /var/opt/mssql/data
   $ sudo su mssql
   $ cp /var/opt/mssql/tmp/* /var/opt/mssql/data/
   $ rm /var/opt/mssql/tmp/*
   $ exit
   ``` 
 
1.  Valide que o SQL Server inicia com êxito com o novo caminho de arquivo. Faça isso em cada nó. Neste ponto somente um nó deve executar o SQL Server por vez. Eles não podem ambos executar ao mesmo tempo porque eles irão tentar acessar os arquivos de dados simultaneamente (para evitar acidentalmente iniciando o SQL Server em ambos os nós, use um recurso de cluster do sistema de arquivos para verificar se que o compartilhamento não está montado duas vezes por nós diferentes). Os comandos a seguir iniciar o SQL Server, verificam o status e, em seguida, interrompa o SQL Server.
 
   ```bash
   sudo systemctl start mssql-server
   sudo systemctl status mssql-server
   sudo systemctl stop mssql-server
   ```
 
Neste ponto, ambas as instâncias do SQL Server estão configuradas para executar com os arquivos de banco de dados no armazenamento compartilhado. A próxima etapa é configurar o SQL Server para Pacemaker. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalar e configurar Pacemaker em cada nó de cluster


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

   > Se você estiver usando outro firewall que não tenha uma configuração de alta disponibilidade interna, as portas a seguir precisarão ser abertas para que o Pacemaker seja capaz de se comunicar com outros nós no cluster
   >
   > * TCP: portas 2224, 3121, 21064
   > * UDP: porta 5405

1. Instale os pacotes do Pacemaker em cada nó.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

   

2. Defina a senha para o usuário padrão criado ao instalar pacotes do Pacemaker e do Corosync. Use a mesma senha em ambos os nós. 

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

## <a name="create-the-cluster"></a>Criar o cluster 

1. Em um de nós, crie o cluster.

   ```bash
   sudo pcs cluster auth <nodeName1 nodeName2 …> -u hacluster
   sudo pcs cluster setup --name <clusterName> <nodeName1 nodeName2 …>
   sudo pcs cluster start --all
   ```

   > RHEL HA tiver agentes de cercamento para VMWare e KVM. Isolamento deve ser desabilitada em todos os outros hipervisores. Desabilitar agentes de isolamento não é recomendável em ambientes de produção. A partir do período de tempo, não existem agentes isolamento para ambientes de nuvem ou o Hyper-v. Se você estiver executando uma dessas configurações, você precisa desabilitar o isolamento. \**Isso não é recomendado em um sistema de produção!**

   O comando a seguir desabilita os agentes de isolamento.

   ```bash
   sudo pcs property set stonith-enabled=false
   sudo pcs property set start-failure-is-fatal=false
   ```

2. Configurar os recursos de cluster do SQL Server, sistema de arquivos e recursos IP virtuais e enviar por push a configuração para o cluster. Você precisa das seguintes informações:

   - **Nome de recurso do SQL Server**: um nome para o recurso de cluster do SQL Server. 
   - **Flutuante nome do recurso IP**: um nome para o recurso de endereço IP virtual.
   - **Endereço IP**: O endereço IP que os clientes usarão para se conectar à instância clusterizada do SQL Server. 
   - **Nome de recurso do sistema de arquivos**: um nome para o recurso de sistema de arquivos.
   - **dispositivo**: caminho de compartilhamento NFS a
   - **dispositivo**: O caminho local que ele está montado para o compartilhamento
   - **fsType**: tipo de compartilhamento de arquivo (ou seja, nfs)

   Atualize os valores do script a seguir para o seu ambiente. Execute em um nó para configurar e iniciar o serviço de cluster.  

   ```bash
   sudo pcs cluster cib cfg 
   sudo pcs -f cfg resource create <sqlServerResourceName> ocf:mssql:fci
   sudo pcs -f cfg resource create <floatingIPResourceName> ocf:heartbeat:IPaddr2 ip=<ip Address>
   sudo pcs -f cfg resource create <fileShareResourceName> Filesystem device=<networkPath> directory=<localPath>         fstype=<fileShareType>
   sudo pcs -f cfg constraint colocation add <virtualIPResourceName> <sqlResourceName>
   sudo pcs -f cfg constraint colocation add <fileShareResourceName> <sqlResourceName> 
   sudo pcs cluster cib-push cfg
   ```

   Por exemplo, o script a seguir cria um recurso de cluster do SQL Server chamado `mssqlha`e um recurso IP flutuante com endereço IP `10.0.0.99`. Ele também cria um recurso do sistema de arquivos e adiciona restrições para que todos os recursos são colocados no mesmo nó que o recurso do SQL. 

   ```bash
   sudo pcs cluster cib cfg
   sudo pcs -f cfg resource create mssqlha ocf:mssql:fci
   sudo pcs -f cfg resource create virtualip ocf:heartbeat:IPaddr2 ip=10.0.0.99
   sudo pcs -f cfg resource create fs Filesystem device="10.8.8.0:/mnt/nfs" directory="/var/opt/mssql/data" fstype="nfs"
   sudo pcs -f cfg constraint colocation add virtualip mssqlha
   sudo pcs -f cfg constraint colocation add fs mssqlha
   sudo pcs cluster cib-push cfg
   ```

   Depois que a configuração seja enviada por push, o SQL Server será iniciado em um nó. 

3. Verifique se o SQL Server é iniciado. 

   ```bash
   sudo pcs status 
   ```

   Os exemplos a seguir mostram os resultados quando Pacemaker com êxito iniciada uma instância clusterizada do SQL Server. 

   ```
   fs     (ocf::heartbeat:Filesystem):    Started sqlfcivm1
   virtualip     (ocf::heartbeat:IPaddr2):      Started sqlfcivm1
   mssqlha  (ocf::mssql:fci): Started sqlfcivm1
   
   PCSD Status:
    slqfcivm1: Online
    sqlfcivm2: Online
   
   Daemon Status:
    corosync: active/disabled
    pacemaker: active/enabled
    pcsd: active/enabled
   ```

## <a name="additional-resources"></a>Recursos adicionais

* [Desde o início do cluster](http://clusterlabs.org/doc/Cluster_from_Scratch.pdf) guia de Pacemaker

## <a name="next-steps"></a>Próximas etapas

[Operar o SQL Server no cluster de disco compartilhado do Red Hat Enterprise Linux](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
