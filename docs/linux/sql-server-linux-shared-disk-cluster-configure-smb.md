---
title: 'Configurar a FCI no armazenamento SMB: SQL Server em Linux'
description: Saiba como configurar uma FCI (instância de cluster de failover) usando o armazenamento SMB do SQL Server em Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 498518fbc119629d2e7da7717b1f6e41c68984ce
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558569"
---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>Configurar a instância de cluster de failover – SMB – SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar o armazenamento SMB para uma FCI (instância de cluster de failover) no Linux. 
 
No mundo não Windows, o SMB é geralmente conhecido como um compartilhamento CIFS (Common Internet File System) e implementado por meio do Samba. No mundo do Windows, o acesso a um compartilhamento SMB é feito desta maneira: \\SERVERNAME\SHARENAME. Para instalações do SQL Server baseadas em Linux, o compartilhamento SMB precisa ser montado como uma pasta.

## <a name="important-source-and-server-information"></a>Informações importantes de origem e servidor

Estas são algumas dicas e observações para usar o SMB com êxito:
- O compartilhamento SMB pode estar no Windows, no Linux ou, até mesmo, em um dispositivo, desde que esteja usando o SMB 3.0 ou superior. Para obter mais informações sobre o Samba e o SMB 3.0, confira [SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0) para ver se a implementação do Samba está em conformidade com o SMB 3.0.
- O compartilhamento SMB deve estar altamente disponível.
- A segurança precisa ser definida corretamente no compartilhamento SMB. Veja abaixo um exemplo de /etc/samba/smb.conf, em que SQLData1 é o nome do compartilhamento.

![05-smbsource][1]

## <a name="instructions"></a>Instruções

1. Escolha um dos servidores que participarão da configuração da FCI. Não importa qual.
   
1. Obtenha informações sobre o usuário mssql.
   
   ```bash
    sudo id mssql
   ```
   
   Anote o UID, o GID e os grupos. 
   
1. Execute `sudo smbclient -L //NameOrIP/ShareName -U User`.
   
   \<NameOrIP> é o nome DNS ou o endereço IP do servidor que hospeda o compartilhamento SMB.
   
   \<ShareName> é o nome do compartilhamento SMB. 
   
1. Para bancos de dados do sistema ou qualquer item armazenado na localização de dados padrão, siga estas etapas. Caso contrário, vá para a etapa 5. 
   
   1. Verifique se o SQL Server está parado no servidor em que você está trabalhando.
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. Alterne totalmente para o superusuário. Você não receberá nenhuma confirmação se tiver êxito.
      
      ```bash
      sudo -i
      ```
      
   1. Alterne para ser o usuário mssql. Você não receberá nenhuma confirmação se tiver êxito.
      
      ```bash
      su mssql
      ```
      
   1. Crie um diretório temporário para armazenar os dados e os arquivos de log do SQL Server. Você não receberá nenhuma confirmação se tiver êxito.
      
      ```bash
      mkdir <TempDir>
      ```
      
      \<TempDir> é o nome da pasta. O exemplo a seguir cria uma pasta chamada /var/opt/mssql/tmp.
      
      ```bash
      mkdir /var/opt/mssql/tmp
      ```
      
   1. Copie os dados e os arquivos de log do SQL Server para o diretório temporário. Você não receberá nenhuma confirmação se tiver êxito.
      
      ```bash
      cp /var/opt/mssql/data/* <TempDir>
      ```
      
      \<TempDir> é o nome da pasta da etapa anterior.
      
   1. Verifique se os arquivos estão no diretório.
      
      ```bash
      ls <TempDir>
      ```
      
      \<TempDir> é o nome da pasta da etapa D.
      
   1. Exclua os arquivos do diretório de dados do SQL Server existente. Você não receberá nenhuma confirmação se tiver êxito.
      
      ```bash
      rm - f /var/opt/mssql/data/*
      ```
      
   1. Verifique se os arquivos foram excluídos. 
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. Digite exit para voltar ao usuário raiz.
      
   1. Monte o compartilhamento SMB na pasta de dados do SQL Server. Você não receberá nenhuma confirmação se tiver êxito. Este exemplo mostra a sintaxe para se conectar a um compartilhamento SMB 3.0 baseado no Windows Server.
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName> é o nome do servidor com o compartilhamento SMB
      
      \<ShareName> é o nome do compartilhamento
      
      \<UserName> é o nome do usuário usado para acessar o compartilhamento
      
      \<Password> é a senha do usuário
      
      \<domain> é o nome do Active Directory
      
      \<mssqlUID> é o UID do usuário mssql 
      
      \<mssqlGID> é o GID do usuário mssql
      
   1. Verifique se a montagem foi bem-sucedida emitindo o comando mount sem opções.
      
      ```bash
      mount
      ```
      
   1. Alterne para o usuário mssql. Você não receberá nenhuma confirmação se tiver êxito.
      
      ```bash
      su mssql
      ```
      
   1. Copie os arquivos do diretório temporário /var/opt/mssql/data. Você não receberá nenhuma confirmação se tiver êxito.
      
      ```bash
      cp /var/opt/mssql/tmp/* /var/opt/mssql/data
      ```
      
   1. Verifique se os arquivos estão lá.
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. Insira exit para não ser o mssql 
      
   1. Insira exit para não ser a raiz
   
   1. Inicie o SQL Server. Se tudo for copiado corretamente e a segurança for aplicada corretamente, o SQL Server deverá ser mostrado como iniciado.
      
      ```bash
      sudo systemctl start mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. Para um teste adicional, crie um banco de dados para garantir que as permissões estejam corretas. O exemplo a seguir usa o Transact-SQL; você poderá usar o SSMS.
      
      ![10_testcreatedb][2] 
      
   1. Interrompa o SQL Server e verifique se ele está desligado. Se desejar adicionar ou testar outros discos, não desligue o SQL Server enquanto eles não forem adicionados e testados.
      
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. Somente se tiver terminado, desmonte o compartilhamento. Caso contrário, desmonte-o depois de concluir o teste/a adição de outros discos.
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName> é o endereço IP ou o nome do host SMB
      
      \<ShareName> é o nome do compartilhamento
      
      \<FolderMountedIn> é o nome da pasta em que o SMB está montado
      
5. Para outros itens que não os bancos de dados do sistema, como bancos de dados de usuário ou backups, siga estas etapas. Se estiver usando apenas a localização padrão, vá para a Etapa 14.
   
   1. Alterne para o superusuário. Você não receberá nenhuma confirmação se tiver êxito.
      
      ```bash
      sudo -i
      ```
      
   1. Crie uma pasta que será usada pelo SQL Server. 
      
      ```bash
      mkdir <FolderName>
      ```
      
      \<FolderName> é o nome da pasta. O caminho completo da pasta precisará ser especificado se não estiver na localização correta. O exemplo a seguir cria uma pasta chamada /var/opt/mssql/userdata.
      
      ```bash
      mkdir /var/opt/mssql/userdata
      ```
      
   1. Monte o compartilhamento SMB na pasta de dados do SQL Server. Você não receberá nenhuma confirmação se tiver êxito. Este exemplo mostra a sintaxe para se conectar a um compartilhamento SMB 3.0 baseado no Samba.
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName> é o nome do servidor com o compartilhamento SMB
      
      \<ShareName> é o nome do compartilhamento
      
      \<FolderName> é o nome da pasta criada na última etapa  
      
      \<UserName> é o nome do usuário usado para acessar o compartilhamento
      
      \<Password> é a senha do usuário
      
      \<mssqlUID> é o UID do usuário mssql
      
      \<mssqlGID> é o GID do usuário mssql.
      
   1. Verifique se a montagem foi bem-sucedida emitindo o comando mount sem opções.
   
   1. Digite exit para deixar de ser o superusuário.
   
   1. Para testar, crie um banco de dados nessa pasta. O exemplo a seguir usa o sqlcmd para criar um banco de dados, alternar o contexto para ele, verificar se os arquivos existem no nível do sistema operacional e, em seguida, exclui a localização temporária. Você pode usar o SSMS.
   
   1. Desmontar o compartilhamento 
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName> é o endereço IP ou o nome do host SMB
      
      \<ShareName> é o nome do compartilhamento
      
      \<FolderMountedIn> é o nome da pasta em que o SMB está montado.
   
1. Repita as etapas nos outros nós.

Agora você está pronto para configurar a FCI.

## <a name="next-steps"></a>Próximas etapas

[Configurar a instância de cluster de failover – SQL Server em Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 
