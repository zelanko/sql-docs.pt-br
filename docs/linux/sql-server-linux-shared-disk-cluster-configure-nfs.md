---
title: "Configurar o armazenamento failover de instância de cluster NFS - SQL Server no Linux | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 368fce4b3c9595f89ea14ca310049a52cf180a28
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2018
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>Configurar a instância de cluster de failover - NFS - SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar o armazenamento NFS para uma instância de cluster de failover (FCI) no Linux. 

NFS ou sistema de arquivos de rede, é um método comum de compartilhamento de discos no mundo Linux, mas não o um Windows. Semelhante a iSCSI, o NFS pode ser configurado em um servidor ou algum tipo de dispositivo ou unidade de armazenamento desde que ele atende aos requisitos de armazenamento para o SQL Server.

## <a name="important-nfs-server-information"></a>Informações importantes do servidor NFS

A fonte de hospedagem NFS (um servidor Linux ou alguma outra coisa) deve ser usando/compatível com a versão 4.2 ou posterior. Versões anteriores não funcionará com o SQL Server no Linux.

Ao configurar as pastas a serem compartilhadas no servidor NFS, certifique-se de que sigam essas opções de diretrizes gerais:
- `rw` para garantir que a pasta pode ser ler e gravados
- `sync` para garantir a garantia de gravações para a pasta
- Não use `no_root_squash` como uma opção; ele é considerado um risco de segurança
- Verifique se que a pasta tem direitos totais (777) aplicados

Certifique-se de que seus padrões de segurança são aplicados para acessar. Ao configurar a pasta, certifique-se de que somente os servidores que participam na FCI deverá ver a pasta NFS. Um exemplo de um /etc/exports modificada em uma solução com base em Linux NFS é mostrado abaixo onde a pasta está restrita a FCIN1 e FCIN2.

![nfsacl 05][1]

## <a name="instructions"></a>Instruções

1. Escolha um dos servidores que participarão na configuração de FCI. Não importa qual delas. 

2. Verifique se o servidor pode ver o mount(s) no servidor NFS.

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer > é o endereço IP do servidor NFS que você pretende usar.

3. Para bancos de dados do sistema ou em qualquer coisa armazenada no local padrão de dados, siga estas etapas. Caso contrário, pule para a etapa 4.
 
   * Certifique-se de que o SQL Server está interrompido no servidor que você está trabalhando.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * Opção totalmente para ser o superusuário. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    sudo -i
    ```

   * Alternar para ser o usuário mssql. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    su mssql
    ```

   * Crie um diretório temporário para armazenar dados do SQL Server e os arquivos de log. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > é o nome da pasta. O exemplo a seguir cria uma pasta chamada /var/opt/mssql/tmp.

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   * Copie os arquivos de log e de dados do SQL Server para o diretório temporário. Você não receberá nenhuma confirmação se for bem-sucedido.
    
    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > é o nome da pasta da etapa anterior.

   * Verifique se os arquivos no diretório.

    ```bash
    ls TempDir
    ```

    \<TempDir > é o nome da pasta da etapa d.

   * Exclua os arquivos do diretório de dados do SQL Server existente. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   * Verifique se que os arquivos foram excluídos. 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * Tipo de saída para alternar novamente para o usuário raiz.

   * Monte o compartilhamento NFS na pasta de dados do SQL Server. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > é o endereço IP do servidor NFS que você pretende usar 

    \<FolderOnNFSServer > é o nome do compartilhamento NFS. A sintaxe de exemplo a seguir corresponde às informações de NFS da etapa 2.

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

   * Verifique se a montagem foi bem-sucedida, emitindo montagem sem opções.

    ```bash
    mount
    ```

    ![10-mountnoswitches][2]

   * Alterne para o usuário mssql. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    su mssql
    ```

   * Copie os arquivos do /var/opt/mssql/data diretório temporário. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssqldata
    ```

   * Verifique se que os arquivos estão lá.

    ```bash
    ls /var/opt/mssql/data
    ```

   * Digite Sair para não ser mssql 
    
   * Digite Sair para não ser raiz

   * Start SQL Server. Se tudo foi copiado corretamente e segurança aplicada corretamente, do SQL Server deve mostrar é iniciado.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * Crie um banco de dados para testar a segurança está configurada corretamente. O exemplo a seguir mostra que está sendo feito por meio do Transact-SQL; Isso pode ser feito por meio do SSMS.
 
    ![CreateTestdatabase][3]

   * Interrompa o SQL Server e verifique se que ele está desligado.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * Se você não estiver criando quaisquer outras montagens NFS, desmonte o compartilhamento. Se você for, não desmonte.

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > é o endereço IP do servidor NFS que você pretende usar

    \<FolderOnNFSServer > é o nome do compartilhamento NFS

    \<FolderMountedIn > é a pasta criada na etapa anterior. 

4. Para tarefas diferentes bancos de dados do sistema, como bancos de dados de usuário ou backups, siga estas etapas. Se apenas usando o local padrão, vá para a etapa 5.

   * Alternar para ser o superusuário. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    sudo -i
    ```

   * Crie uma pasta que será usada pelo SQL Server. 

    ```bash
    mkdir <FolderName>
    ```

    \<Nome da pasta > é o nome da pasta. Caminho completo da pasta deve ser especificado se não está no local correto. O exemplo a seguir cria uma pasta chamada /var/opt/mssql/userdata.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   * Monte o compartilhamento NFS na pasta que foi criado na etapa anterior. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > é o endereço IP do servidor NFS que você pretende usar

    \<FolderOnNFSServer > é o nome do compartilhamento NFS

    \<FolderToMountIn > é a pasta criada na etapa anterior. Abaixo está um exemplo. 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * Verifique se a montagem foi bem-sucedida, emitindo montagem sem opções.
  
   * Tipo de saída não seja o superusuário.

   * Para testar, crie um banco de dados nessa pasta. O exemplo a seguir usa o sqlcmd para criar um banco de dados, alterne o contexto para ele, verifique se os arquivos existem no nível do sistema operacional e, em seguida, exclui o local temporário. Você pode usar o SSMS.

    ![15-createtestdatabase][4]
 
   * Desmontar o compartilhamento 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > é o endereço IP do servidor NFS que você pretende usar
    
    \<FolderOnNFSServer > é o nome do compartilhamento NFS

    \<FolderMountedIn > é a pasta criada na etapa anterior. Abaixo está um exemplo. 
 
5. Repita as etapas nos outros nós.


## <a name="next-steps"></a>Próximas etapas

[Configurar a instância de cluster de failover - SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
