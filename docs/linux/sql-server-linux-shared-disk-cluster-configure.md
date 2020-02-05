---
title: 'Configurar a FCI: SQL Server em Linux (RHEL)'
description: Saiba como configurar uma FCI (instância de cluster de failover) RHEL (Red Hat Enterprise Linux) no SQL Server.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 61fe5d7ffb5dfc6ec98f6d5350eff396deaa0312
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558321"
---
# <a name="configure-failover-cluster-instance---sql-server-on-linux-rhel"></a>Configurar a instância de cluster de failover – SQL Server em Linux (RHEL)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Uma instância de cluster de failover de disco compartilhado de dois nós do SQL Server fornece redundância no nível do servidor para alta disponibilidade. Neste tutorial, você aprenderá a criar uma instância de cluster de failover de dois nós do SQL Server em Linux. As etapas específicas que serão concluídas incluem:

> [!div class="checklist"]
> * Instalar e configurar o Linux
> * Instalar e configurar o SQL Server
> * Configurar o arquivo de hosts
> * Configurar o armazenamento compartilhado e mover os arquivos de banco de dados
> * Instalar e configurar o Pacemaker em cada nó de cluster
> * Configurar a instância de cluster de failover

Este artigo explica como criar uma FCI (instância de cluster de failover) de disco compartilhado de dois nós para o SQL Server. O artigo inclui instruções e exemplos de script para o RHEL (Red Hat Enterprise Linux). As distribuições do Ubuntu são semelhantes ao RHEL, portanto, os exemplos de script normalmente também funcionarão no Ubuntu. 

Para obter informações conceituais, confira [FCI (instância de cluster de failover) do SQL Server no Linux](sql-server-linux-shared-disk-cluster-concepts.md).

## <a name="prerequisites"></a>Prerequisites

Para concluir o cenário de ponta a ponta a seguir, você precisará de dois computadores para implantar o cluster de dois nós e outro servidor para armazenamento. As etapas abaixo descrevem como esses servidores serão configurados.

## <a name="set-up-and-configure-linux"></a>Instalar e configurar o Linux

A primeira etapa é configurar o sistema operacional nos nós de cluster. Em cada nó no cluster, configure uma distribuição do Linux. Use a mesma distribuição e versão em ambos os nós. Use uma ou outra das seguintes distribuições:
    
* RHEL com uma assinatura válida para o complemento de HA

## <a name="install-and-configure-sql-server"></a>Instalar e configurar o SQL Server

1. Instale e configure o SQL Server em ambos os nós.  Para obter instruções detalhadas, confira [Instalar o SQL Server em Linux](sql-server-linux-setup.md).
1. Designe um nó como primário e o outro como secundário para fins de configuração. Use esses termos para seguir este guia.  
1. No nó secundário, interrompa e desabilite o SQL Server.
    O seguinte exemplo interrompe e desabilita o SQL Server: 
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE] 
    > No momento da instalação, uma Chave Mestra do Servidor é gerada para a Instância do SQL Server e colocada em `var/opt/mssql/secrets/machine-key`. No Linux, o SQL Server sempre é executado como uma conta local chamada mssql. Como é uma conta local, a identidade dela não é compartilhada entre os nós. Portanto, você precisa copiar a chave de criptografia do nó primário para cada nó secundário, de modo que cada conta mssql local possa acessá-la para descriptografar a Chave Mestra do Servidor. 

1.  No nó primário, crie um logon do SQL Server para o Pacemaker e conceda a permissão de logon para executar `sp_server_diagnostics`. O Pacemaker usa essa conta para verificar qual nó está executando o SQL Server. 

    ```bash
    sudo systemctl start mssql-server
    ```
   
   Conecte-se ao banco de dados `master` do SQL Server com a conta SA e execute o seguinte:

   ```sql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```

   Alternativamente, você pode definir as permissões em um nível mais granular. O logon do Pacemaker exige que `VIEW SERVER STATE` consulte o status de integridade com sp_server_diagnostics e que `setupadmin` e `ALTER ANY LINKED SERVER` atualizem o nome da instância de FCI com o nome do recurso executando sp_dropserver e sp_addserver. 

1. No nó primário, interrompa e desabilite o SQL Server. 

## <a name="configure-the-hosts-file"></a>Configurar o arquivo de hosts

Em cada nó de cluster, configure o arquivo de hosts. O arquivo de hosts precisa incluir o endereço IP e o nome de cada nó de cluster.

1. Verifique o endereço IP de cada nó. O script a seguir mostra o endereço IP do nó atual. 

    ```bash
    sudo ip addr show
    ```

1. Defina o nome do computador em cada nó. Dê a cada nó um nome exclusivo que tenha 15 caracteres ou menos. Defina o nome do computador adicionando-o a `/etc/hosts`. O script a seguir permite que você edite `/etc/hosts` com `vi`. 

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

## <a name="configure-storage--move-database-files"></a>Configurar o armazenamento e mover os arquivos de banco de dados  

Você precisa fornecer um armazenamento ao qual ambos os nós possam ter acesso. Você pode usar o iSCSI, o NFS ou o SMB. Configure o armazenamento, apresente o armazenamento para os nós de cluster e, em seguida, mova os arquivos de banco de dados para o novo armazenamento. Os seguintes artigos explicam as etapas para cada tipo de armazenamento:

- [Configurar a instância de cluster de failover – iSCSI – SQL Server em Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [Configurar a instância de cluster de failover – NFS – SQL Server em Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [Configurar a instância de cluster de failover – SMB – SQL Server em Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)

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

   > Se você estiver usando outro firewall que não tenha uma configuração de alta disponibilidade interna, as portas a seguir precisarão ser abertas para que o Pacemaker possa se comunicar com outros nós no cluster
   >
   > * TCP: portas 2224, 3121, 21064
   > * UDP: porta 5405

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

A FCI será criada em um grupo de recursos. Isso é um pouco mais fácil, pois o grupo de recursos atenua a necessidade de restrições. No entanto, adicione os recursos ao grupo de recursos na ordem em que eles devem ser iniciados. A ordem em que eles devem ser iniciados é: 

1. Recurso de armazenamento
2. Recurso de rede
3. Recurso de aplicativo

Este exemplo criará uma FCI no grupo NewLinFCIGrp. O nome do grupo de recursos precisa ser exclusivo em qualquer recurso criado no Pacemaker.

1.  Crie o recurso de disco. Você não receberá nenhuma resposta se não houver nenhum problema. A maneira de criar o recurso de disco depende do tipo de armazenamento. Veja a seguir um exemplo de cada tipo de armazenamento. Use o exemplo que se aplica ao tipo de armazenamento do armazenamento clusterizado.

    **iSCSI**

    ```bash
    sudo pcs resource create <iSCSIDiskResourceName> Filesystem device="/dev/<VolumeGroupName>/<LogicalVolumeName>" directory="<FolderToMountiSCSIDisk>" fstype="<FileSystemType>" --group RGName
    ```

    \<iSCSIDIskResourceName> é o nome do recurso associado ao disco iSCSI

    \<VolumeGroupName> é o nome do grupo de volume  

    \<LogicalVolumeName> é o nome do volume lógico que foi criado  

    \<FolderToMountiSCSIDIsk> é a pasta para montar o disco (para bancos de dados do sistema e a localização padrão, ela é /var/opt/mssql/data)

    \<FileSystemType> seria EXT4 ou XFS dependendo de como tudo estava formatado e ao que a distribuição dá suporte. 

    **NFS**

    ```bash
    sudo pcs resource create <NFSDiskResourceName> Filesystem device="<IPAddressOfNFSServer>:<FolderOnNFSServer>" directory="<FolderToMountNFSShare>" fstype=nfs4 options=" nfsvers=4.2,timeo=14,intr" --group RGName
    mount -t nfs4 IPAddressOfNFSServer:FolderOnNFSServer /var/opt/mssql/data -o 
    ```

    \<NFSDIskResourceName> é o nome do recurso associado ao compartilhamento NFS

    \<IPAddressOfNFSServer> é o endereço IP do servidor NFS que você usará

    \<FolderOnNFSServer> é o nome do compartilhamento NFS

    \<FolderToMountNFSShare> é a pasta para montar o disco (para bancos de dados do sistema e a localização padrão, ela é /var/opt/mssql/data)

    Um exemplo é mostrado aqui:

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    **SMB**

    ```bash
    sudo pcs resource create SMBDiskResourceName Filesystem device="//<ServerName>/<ShareName>" directory="<FolderName>" fstype=cifs options="vers=3.0,username=<UserName>,password=<Password>,domain=<ADDomain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777" --group <RGName>
    ```

    \<ServerName> é o nome do servidor com o compartilhamento SMB

    \<ShareName> é o nome do compartilhamento

    \<FolderName> é o nome da pasta criada na última etapa
    
    \<UserName> é o nome do usuário usado para acessar o compartilhamento

    \<Password> é a senha do usuário

    \<ADDomain> é o domínio do AD DS (se aplicável, ao usar um compartilhamento SMB baseado no Windows Server)

    \<mssqlUID> é o UID do usuário mssql

    \<mssqlGID> é o GID do usuário mssql

    \<RGName> é o nome do grupo de recursos
 
2.  Crie o endereço IP que será usado pela FCI. Você não receberá nenhuma resposta se não houver nenhum problema.

    ```bash
    sudo pcs resource create <IPResourceName> ocf:heartbeat:IPaddr2 ip=<IPAddress> nic=<NetworkCard> cidr_netmask=<NetMask> --group <RGName>
    ```

    \<IPResourceName> é o nome do recurso associado ao endereço IP

    \<IPAddress> é o endereço IP da FCI

    \<NetworkCard> é a placa de rede associada à sub-rede (ou seja, eth0)

    \<NetMask> é a máscara de rede da sub-rede (ou seja, 24)

    \<RGName> é o nome do grupo de recursos
 
3.  Crie o recurso da FCI. Você não receberá nenhuma resposta se não houver nenhum problema.

    ```bash
    sudo pcs resource create FCIResourceName ocf:mssql:fci op defaults timeout=60s --group RGName
    ```

    \<FCIResourceName> não é apenas o nome do recurso, mas o nome amigável associado à FCI. Isso é o que os usuários e os aplicativos usarão para se conectar. 

    \<RGName> é o nome do grupo de recursos.
 
4.  Execute o comando `sudo pcs resource`. A FCI deve estar online.
 
5.  Conecte-se à FCI com o SSMS ou o sqlcmd usando o nome de recurso/DNS da FCI.

6.  Emita a instrução `SELECT @@SERVERNAME`. Ela deverá retornar o nome da FCI.

7.  Emita a instrução `SELECT SERVERPROPERTY('ComputerNamePhysicalNetBIOS')`. Ela deverá retornar o nome do nó no qual a FCI está sendo executada.

8.  Faça failover manual da FCI para os outros nós. Confira as instruções em [Operar a instância de cluster de failover– SQL Server em Linux](sql-server-linux-shared-disk-cluster-operate.md).

9.  Por fim, faça failback da FCI para o nó original e remova a restrição de colocalização.

<!---

|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)

-->
## <a name="summary"></a>Resumo

Neste tutorial, você concluiu as tarefas a seguir.

> [!div class="checklist"]
> * Instalar e configurar o Linux
> * Instalar e configurar o SQL Server
> * Configurar o arquivo de hosts
> * Configurar o armazenamento compartilhado e mover os arquivos de banco de dados
> * Instalar e configurar o Pacemaker em cada nó de cluster
> * Configurar a instância de cluster de failover

## <a name="next-steps"></a>Próximas etapas

- [Operar a instância de cluster de failover – SQL Server em Linux](sql-server-linux-shared-disk-cluster-operate.md)

<!--Image references-->
