---
title: Configurar a instância de cluster de failover – SQL Server no Linux (RHEL)
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 407e1e11bcaf2c1b7ffe0426c6a3c7493e71bc74
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833160"
---
# <a name="configure-failover-cluster-instance---sql-server-on-linux-rhel"></a>Configurar a instância de cluster de failover – SQL Server no Linux (RHEL)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Uma instância de cluster de failover de disco compartilhado de dois nós do SQL Server fornece redundância para alta disponibilidade em nível de servidor. Neste tutorial, você aprenderá como criar uma instância de cluster de failover com dois nós do SQL Server no Linux. As etapas específicas que serão concluídas incluem:

> [!div class="checklist"]
> * Instalar e configurar o Linux
> * Instalar e configurar o SQL Server
> * Configurar o arquivo de hosts
> * Configurar o armazenamento compartilhado e mover os arquivos de banco de dados
> * Instalar e configurar o Pacemaker em cada nó de cluster
> * Configurar a instância de cluster de failover

Este artigo explica como criar uma instância de cluster de failover (FCI do) disco compartilhado de dois nós para o SQL Server. O artigo inclui instruções e exemplos de script para o Red Hat Enterprise Linux (RHEL). Distribuições Ubuntu são semelhantes para RHEL, portanto, os exemplos de script serão normalmente também funcionam no Ubuntu. 

Para obter informações conceituais, consulte [SQL Server Failover Cluster FCI (instância) no Linux](sql-server-linux-shared-disk-cluster-concepts.md).

## <a name="prerequisites"></a>Pré-requisitos

Para concluir o seguinte cenário de ponta a ponta, você precisa de duas máquinas para implantar o cluster de dois nós e outro servidor para o armazenamento. As etapas a seguir descrevem como esses servidores serão configurados.

## <a name="set-up-and-configure-linux"></a>Instalar e configurar o Linux

A primeira etapa é configurar o sistema operacional em nós de cluster. Em cada nó no cluster, configure uma distribuição do linux. Use a distribuição e a versão mesmo em ambos os nós. Use um ou outro das seguintes distribuições:
    
* RHEL com uma assinatura válida para o complemento de alta disponibilidade

## <a name="install-and-configure-sql-server"></a>Instalar e configurar o SQL Server

1. Instale e configure o SQL Server em ambos os nós.  Para obter instruções detalhadas, consulte [instalar o SQL Server no Linux](sql-server-linux-setup.md).
1. Designe um nó como primário e o outro como secundário, para fins de configuração. Usar esses termos para os seguintes itens neste guia.  
1. No nó secundário, interrompa e desabilite o SQL Server.
    O exemplo a seguir interrompe e desabilita o SQL Server: 
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE] 
    > No conjunto de tempo de atividade, uma chave mestra do servidor é gerada para a instância do SQL Server e colocado no `var/opt/mssql/secrets/machine-key`. No Linux, SQL Server sempre é executado como uma conta local chamada mssql. Porque é uma conta local, sua identidade não é compartilhada entre os nós. Portanto, você precisará copiar a chave de criptografia do nó principal para cada nó secundário, portanto, cada conta mssql local pode acessá-lo para descriptografar a chave mestra do servidor. 

1.  No nó primário, crie um logon do SQL server para Pacemaker e conceder a permissão de logon para executar `sp_server_diagnostics`. O pacemaker usa essa conta para verificar qual nó está executando o SQL Server. 

    ```bash
    sudo systemctl start mssql-server
    ```
   
   Conectar-se ao SQL Server `master` de banco de dados com a conta sa e execute o seguinte:

   ```sql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```

   Alternativamente, você pode definir as permissões em um nível mais granular. O logon de Pacemaker requer `VIEW SERVER STATE` consultar o status de integridade com sp_server_diagnostics, `setupadmin` e `ALTER ANY LINKED SERVER` para atualizar o nome da instância FCI com o nome do recurso executando sp_dropserver e sp_addserver. 

1. No nó primário, interrompa e desabilite o SQL Server. 

## <a name="configure-the-hosts-file"></a>Configurar o arquivo de hosts

Em cada nó de cluster, configure o arquivo de hosts. O arquivo de hosts deve incluir o endereço IP e o nome de cada nó do cluster.

1. Verifique o endereço IP para cada nó. O script a seguir mostra o endereço IP do nó atual. 

    ```bash
    sudo ip addr show
    ```

1. Defina o nome do computador em cada nó. Dê a cada nó de um nome exclusivo que é de 15 caracteres ou menos. Definir o nome do computador, adicionando-o para `/etc/hosts`. O script a seguir permite que você edite `/etc/hosts` com `vi`. 

   ```bash
   sudo vi /etc/hosts
   ```
   A exemplo a seguir mostra `/etc/hosts` com adições para dois nós denominados `sqlfcivm1` e `sqlfcivm2`.

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

## <a name="configure-storage--move-database-files"></a>Configurar o armazenamento de & mover arquivos de banco de dados  

Você precisa fornecer armazenamento que ambos os nós podem acessar. Você pode usar iSCSI, NFS ou SMB. Configurar o armazenamento, apresentar o armazenamento a nós do cluster e, em seguida, mova os arquivos de banco de dados para o novo armazenamento. Os artigos a seguir explicam as etapas para cada tipo de armazenamento:

- [Configurar a instância de cluster de failover - iSCSI – SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [Configurar a instância de cluster de failover - NFS – SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [Configurar a instância de cluster de failover - SMB – SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalar e configurar o Pacemaker em cada nó de cluster

1. Em ambos os nós de cluster, crie um arquivo para armazenar o nome de usuário do SQL Server e a senha para o logon do Pacemaker. 

    O comando a seguir cria e popula este arquivo:

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd    
    ```

1. Em ambos os nós de cluster, abra as portas de firewall do Pacemaker. Para abrir essas portas com o `firewalld`, execute o seguinte comando:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > Se você estiver usando outro firewall que não tem uma configuração de alta disponibilidade interna, as seguintes portas precisam ser abertas para o Pacemaker seja capaz de se comunicar com outros nós no cluster
   >
   > * TCP: Ports 2224, 3121, 21064
   > * UDP: Porta 5405

1. Instale os pacotes do Pacemaker em cada nó.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```
1. Defina a senha do usuário padrão criado ao instalar pacotes do Pacemaker e do Corosync. Use a mesma senha em ambos os nós. 

   ```bash
   sudo passwd hacluster
   ```
1. Habilite e inicie o serviço `pcsd` e o Pacemaker. Isso permitirá que os nós reingressem no cluster após a reinicialização. Execute o comando a seguir em ambos os nós.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

1. Instalar o agente do recurso FCI para SQL Server. Execute os comandos a seguir em ambos os nós. 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="configure-the-failover-cluster-instance"></a>Configurar a instância de cluster de failover

A FCI será criada em um grupo de recursos. Isso é um pouco mais fácil, pois o grupo de recursos reduz a necessidade de restrições. No entanto, adicione os recursos no grupo de recursos na ordem em que eles devem iniciar. A ordem em que eles devem iniciar é: 

1. Recurso de armazenamento
2. Recurso de rede
3. Recurso de aplicativo

Este exemplo criará uma FCI no grupo NewLinFCIGrp. O nome do grupo de recursos deve ser exclusivo de qualquer recurso criado no Pacemaker.

1.  Crie o recurso de disco. Se não houver um problema, você obterá sem resposta. A maneira de criar o recurso de disco depende do tipo de armazenamento. O exemplo a seguir é um exemplo para cada tipo de armazenamento. Use o exemplo que aplica-se para o tipo de armazenamento para seu armazenamento em cluster.

    **iSCSI**

    ```bash
    sudo pcs resource create <iSCSIDiskResourceName> Filesystem device="/dev/<VolumeGroupName>/<LogicalVolumeName>" directory="<FolderToMountiSCSIDisk>" fstype="<FileSystemType>" --group RGName
    ```

    \<iSCSIDIskResourceName > é o nome do recurso associado com o disco iSCSI

    \<VolumeGroupName > é o nome do grupo de volumes  

    \<LogicalVolumeName > é o nome do volume lógico que foi criado  

    \<FolderToMountiSCSIDIsk > é a pasta para montar o disco (para bancos de dados do sistema e o local padrão, ele seria /var/opt/mssql/data)

    \<FileSystemType > seria EXT4 ou XFS dependendo de como as coisas foram formatadas e dá suporte à qual a distribuição. 

    **NFS**

    ```bash
    sudo pcs resource create <NFSDiskResourceName> Filesystem device="<IPAddressOfNFSServer>:<FolderOnNFSServer>" directory="<FolderToMountNFSShare>" fstype=nfs4 options=" nfsvers=4.2,timeo=14,intr" --group RGName
    mount -t nfs4 IPAddressOfNFSServer:FolderOnNFSServer /var/opt/mssql/data -o 
    ```

    \<NFSDIskResourceName > é o nome do recurso associado com o compartilhamento NFS

    \<IPAddressOfNFSServer > é o endereço IP do servidor NFS que você pretende usar

    \<FolderOnNFSServer > é o nome do compartilhamento de NFS

    \<FolderToMountNFSShare > é a pasta para montar o disco (para bancos de dados do sistema e o local padrão, ele seria /var/opt/mssql/data)

    Um exemplo é mostrado aqui:

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    **SMB**

    ```bash
    sudo pcs resource create SMBDiskResourceName Filesystem device="//<ServerName>/<ShareName>" directory="<FolderName>" fstype=cifs options="vers=3.0,username=<UserName>,password=<Password>,domain=<ADDomain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777" --group <RGName>
    ```

    \<ServerName > é o nome do servidor com o compartilhamento SMB

    \<Nome de compartilhamento > é o nome do compartilhamento

    \<Nome da pasta > é o nome da pasta criada na última etapa
    
    \<Nome de usuário > é o nome do usuário para acessar o compartilhamento

    \<Senha > é a senha do usuário

    \<ADDomain > é o domínio de AD DS (se aplicável ao usar um compartilhamento SMB baseados no Windows Server)

    \<mssqlUID > é o UID do usuário mssql

    \<mssqlGID > é o GID do usuário mssql

    \<RGName > é o nome do grupo de recursos
 
2.  Crie o endereço IP que será usado pela FCI. Se não houver um problema, você obterá sem resposta.

    ```bash
    sudo pcs resource create <IPResourceName> ocf:heartbeat:IPaddr2 ip=<IPAddress> nic=<NetworkCard> cidr_netmask=<NetMask> --group <RGName>
    ```

    \<IPResourceName > é o nome do recurso associado com o endereço IP

    \<IPAddress > é o endereço IP para a FCI

    \<NetworkCard > é a placa de rede associada à sub-rede (ou seja, eth0)

    \<Máscara de rede > é a máscara de rede da sub-rede (ou seja, 24)

    \<RGName > é o nome do grupo de recursos
 
3.  Crie o recurso FCI. Se não houver um problema, você obterá sem resposta.

    ```bash
    sudo pcs resource create FCIResourceName ocf:mssql:fci op defaults timeout=60s --group RGName
    ```

    \<FCIResourceName > é não apenas o nome do recurso, mas o nome amigável que está associado com a FCI. Isso é o que os usuários e aplicativos usará para se conectar. 

    \<RGName > é o nome do grupo de recursos.
 
4.  Execute o comando `sudo pcs resource`. A FCI deve estar online.
 
5.  Conecte-se à FCI com o SSMS ou usando o nome DNS/recurso da FCI do sqlcmd.

6.  Emita a instrução `SELECT @@SERVERNAME`. Ele deverá retornar o nome da FCI.

7.  Emita a instrução `SELECT SERVERPROPERTY('ComputerNamePhysicalNetBIOS')`. Ele deverá retornar o nome do nó que a FCI está sendo executado.

8.  Executar manualmente a FCI para o outro nó (s). Consulte as instruções em [instância de cluster de failover Operate - SQL Server no Linux](sql-server-linux-shared-disk-cluster-operate.md).

9.  Por fim, falhar a FCI para o nó original e remova a restrição de colocação.

<!---

|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)

-->
## <a name="summary"></a>Resumo

Neste tutorial, você concluiu as seguintes tarefas.

> [!div class="checklist"]
> * Instalar e configurar o Linux
> * Instalar e configurar o SQL Server
> * Configurar o arquivo de hosts
> * Configurar o armazenamento compartilhado e mover os arquivos de banco de dados
> * Instalar e configurar o Pacemaker em cada nó de cluster
> * Configurar a instância de cluster de failover

## <a name="next-steps"></a>Próximas etapas

- [Operar a instância de cluster de failover – SQL Server no Linux](sql-server-linux-shared-disk-cluster-operate.md)

<!--Image references-->
