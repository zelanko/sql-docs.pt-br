---
title: Configurar o armazenamento NFS da instância de cluster de failover – SQL Server em Linux
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 1088060b8f1af418f14210b7e09a6641fc3a62d8
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032360"
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>Configurar a instância de cluster de failover – NFS – SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar o armazenamento NFS para uma FCI (instância de cluster de failover) no Linux. 

NFS, ou Network File System, é um método comum de compartilhamento de discos no mundo Linux, mas não do Windows. Semelhante ao iSCSI, o NFS pode ser configurado em um servidor ou algum tipo de dispositivo ou unidade de armazenamento, contanto que atenda aos requisitos de armazenamento para SQL Server.

## <a name="important-nfs-server-information"></a>Informações importantes do servidor NFS

O NFS de hospedagem de origem (um servidor Linux ou algo diferente) deve estar usando/em conformidade com a versão 4.2 ou posterior. As versões anteriores não funcionarão com o SQL Server em Linux.

Ao configurar as pastas a serem compartilhadas no servidor NFS, siga estas opções gerais de diretrizes:
- `rw` para garantir que seja possível ler a pasta e gravar nela
- `sync` para assegurar gravações garantidas na pasta
- Não use `no_root_squash` como opção; isso é considerado um risco de segurança
- Verifique se a pasta tem direitos totais (777) aplicados

Verifique se seus padrões de segurança foram impostos para acesso. Ao configurar a pasta, verifique se apenas os servidores que participam do FCI devem ver a pasta NFS. Um exemplo de um /etc/exports modificado em uma solução NFS baseada em Linux é mostrado abaixo, em que a pasta está restrita a FCIN1 e FCIN2.

![05-nfsacl][1]

## <a name="instructions"></a>Instruções

1. Escolha um dos servidores que participarão da configuração da FCI. Não importa qual. 

2. Verifique se o servidor pode ver as montagens no servidor NFS.

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer> é o endereço IP do servidor NFS que você vai usar.

3. Para bancos de dados do sistema ou qualquer item armazenado na localização de dados padrão, siga estas etapas. Caso contrário, vá para a etapa 4.
 
   * Verifique se o SQL Server está parado no servidor em que você está trabalhando.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * Alterne totalmente para o superusuário. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    sudo -i
    ```

   * Alterne para ser o usuário mssql. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    su mssql
    ```

   * Crie um diretório temporário para armazenar os dados e os arquivos de log do SQL Server. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir> é o nome da pasta. O exemplo a seguir cria uma pasta chamada /var/opt/mssql/tmp.

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   * Copie os dados e os arquivos de log do SQL Server para o diretório temporário. Você não receberá nenhuma confirmação se tiver êxito.
    
    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir> é o nome da pasta da etapa anterior.

   * Verifique se os arquivos estão no diretório.

    ```bash
    ls TempDir
    ```

    \<TempDir> é o nome da pasta da etapa D.

   * Exclua os arquivos do diretório de dados do SQL Server existente. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    rm - f /var/opt/mssql/data/*
    ```

   * Verifique se os arquivos foram excluídos. 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * Digite exit para voltar ao usuário raiz.

   * Monte o compartilhamento NFS na pasta de dados do SQL Server. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer> é o endereço IP do servidor NFS que você usará 

    \<FolderOnNFSServer> é o nome do compartilhamento NFS. A sintaxe de exemplo a seguir corresponde às informações de NFS da Etapa 2.

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

   * Verifique se a montagem foi bem-sucedida emitindo o comando mount sem opções.

    ```bash
    mount
    ```

    ![10-mountnoswitches][2]

   * Alterne para o usuário mssql. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    su mssql
    ```

   * Copie os arquivos do diretório temporário /var/opt/mssql/data. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssqldata
    ```

   * Verifique se os arquivos estão lá.

    ```bash
    ls /var/opt/mssql/data
    ```

   * Insira exit para não ser o mssql 
    
   * Insira exit para não ser a raiz

   * Inicie o SQL Server. Se tudo for copiado corretamente e a segurança for aplicada corretamente, o SQL Server deverá ser mostrado como iniciado.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * Crie um banco de dados para testar se a segurança está configurada corretamente. O exemplo a seguir mostra isso sendo feito por meio do Transact-SQL. Isso pode ser feito por meio do SSMS.
 
    ![CreateTestdatabase][3]

   * Interrompa o SQL Server e verifique se ele está desligado.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * Se você não estiver criando nenhuma outra montagem NFS, desmonte o compartilhamento. Se estiver, não desmonte.

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer> é o endereço IP do servidor NFS que você usará

    \<FolderOnNFSServer> é o nome do compartilhamento NFS

    \<FolderMountedIn > é a pasta criada na etapa anterior. 

4. Para outros itens que não os bancos de dados do sistema, como bancos de dados de usuário ou backups, siga estas etapas. Se estiver usando apenas a localização padrão, vá para a Etapa 5.

   * Alterne para o superusuário. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    sudo -i
    ```

   * Crie uma pasta que será usada pelo SQL Server. 

    ```bash
    mkdir <FolderName>
    ```

    \<FolderName> é o nome da pasta. O caminho completo da pasta precisará ser especificado se não estiver na localização correta. O exemplo a seguir cria uma pasta chamada /var/opt/mssql/userdata.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   * Monte o compartilhamento NFS na pasta que foi criada na etapa anterior. Você não receberá nenhuma confirmação se tiver êxito.

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer> é o endereço IP do servidor NFS que você usará

    \<FolderOnNFSServer> é o nome do compartilhamento NFS

    \<FolderToMountIn > é a pasta criada na etapa anterior. Veja abaixo um exemplo. 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * Verifique se a montagem foi bem-sucedida emitindo o comando mount sem opções.
  
   * Digite exit para deixar de ser o superusuário.

   * Para testar, crie um banco de dados nessa pasta. O exemplo a seguir usa o sqlcmd para criar um banco de dados, alternar o contexto para ele, verificar se os arquivos existem no nível do sistema operacional e, em seguida, exclui a localização temporária. Você pode usar o SSMS.

    ![15-createtestdatabase][4]
 
   * Desmontar o compartilhamento 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer> é o endereço IP do servidor NFS que você usará
    
    \<FolderOnNFSServer> é o nome do compartilhamento NFS

    \<FolderMountedIn > é a pasta criada na etapa anterior. Veja abaixo um exemplo. 
 
5. Repita as etapas nos outros nós.


## <a name="next-steps"></a>Próximas etapas

[Configurar a instância de cluster de failover – SQL Server em Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
