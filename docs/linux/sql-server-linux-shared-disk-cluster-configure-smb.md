---
title: Configurar o failover cluster instância armazenamento SMB – SQL Server no Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 802634ff8a62134433185913fd1fd3374df1680a
ms.sourcegitcommit: 02df4e7965b2a858030bb508eaf8daa9bc10b00b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66265584"
---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>Configurar a instância de cluster de failover - SMB – SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar o armazenamento SMB para uma instância de cluster de failover (FCI) no Linux. 
 
No mundo não Windows, SMB é geralmente conhecido para como o Common Internet File System (CIFS) compartilhar e implementado por meio do Samba. No mundo do Windows, acessar um compartilhamento SMB é feito dessa forma: \\SERVERNAME\SHARENAME. Para instalações do SQL Server baseado em Linux, o compartilhamento SMB deve ser montado como uma pasta.

## <a name="important-source-and-server-information"></a>Informações importantes de origem e de servidor

Aqui estão algumas dicas e notas de uso de SMB com êxito:
- O compartilhamento SMB pode ser no Windows, Linux, ou até mesmo de um dispositivo como desde que ele está usando o SMB 3.0 ou superior. Para obter mais informações sobre o Samba e SMB 3.0, consulte [SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0) para ver se sua implementação do Samba é compatível com SMB 3.0.
- O compartilhamento SMB deve estar altamente disponível.
- Segurança deve ser definida corretamente no compartilhamento SMB. Abaixo está um exemplo de /etc/samba/smb.conf, onde SQLData1 é o nome do compartilhamento.

![smbsource 05][1]

## <a name="instructions"></a>Instruções

1. Escolha um dos servidores que participarão na configuração de FCI. Não importa qual delas.
   
1. Obter informações sobre o usuário mssql.
   
   ```bash
    sudo id mssql
   ```
   
   Observe o uid, gid e grupos. 
   
1. Executar `sudo smbclient -L //NameOrIP/ShareName -U User`.
   
   \<NameOrIP > é o nome DNS ou endereço IP do servidor que hospeda o compartilhamento SMB.
   
   \<Nome de compartilhamento > é o nome do compartilhamento SMB. 
   
1. Para o sistema de bancos de dados ou qualquer coisa armazenada no local de dados padrão siga estas etapas. Caso contrário, pule para a etapa 5. 
   
   1. Verifique se o SQL Server é interrompido no servidor que você está trabalhando.
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. Alternar totalmente para ser o superusuário. Você não receberá qualquer confirmação se for bem-sucedido.
      
      ```bash
      sudo -i
      ```
      
   1. Opção a ser o usuário mssql. Você não receberá qualquer confirmação se for bem-sucedido.
      
      ```bash
      su mssql
      ```
      
   1. Crie um diretório temporário para armazenar os dados do SQL Server e arquivos de log. Você não receberá qualquer confirmação se for bem-sucedido.
      
      ```bash
      mkdir <TempDir>
      ```
      
      \<TempDir > é o nome da pasta. O exemplo a seguir cria uma pasta chamada /var/opt/mssql/tmp.
      
      ```bash
      mkdir /var/opt/mssql/tmp
      ```
      
   1. Copie os arquivos de log e de dados do SQL Server para o diretório temporário. Você não receberá qualquer confirmação se for bem-sucedido.
      
      ```bash
      cp /var/opt/mssql/data/* <TempDir>
      ```
      
      \<TempDir > é o nome da pasta da etapa anterior.
      
   1. Verifique se os arquivos no diretório.
      
      ```bash
      ls <TempDir>
      ```
      
      \<TempDir > é o nome da pasta da etapa d.
      
   1. Exclua os arquivos do diretório de dados do SQL Server existente. Você não receberá qualquer confirmação se for bem-sucedido.
      
      ```bash
      rm - f /var/opt/mssql/data/*
      ```
      
   1. Verifique se que os arquivos foram excluídos. 
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. Digite exit para alternar novamente para o usuário raiz.
      
   1. Monte o compartilhamento SMB na pasta de dados do SQL Server. Você não receberá qualquer confirmação se for bem-sucedido. Este exemplo mostra a sintaxe para se conectar a um compartilhamento SMB 3.0 de baseados no Windows Server.
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName > é o nome do servidor com o compartilhamento SMB
      
      \<Nome de compartilhamento > é o nome do compartilhamento
      
      \<Nome de usuário > é o nome do usuário para acessar o compartilhamento
      
      \<Senha > é a senha do usuário
      
      \<domínio > é o nome do Active Directory
      
      \<mssqlUID > é o UID do usuário mssql 
      
      \<mssqlGID > é o GID do usuário mssql
      
   1. Verifique se a montagem foi bem-sucedida, emitindo montagem sem opções.
      
      ```bash
      mount
      ```
      
   1. Alterne para o usuário mssql. Você não receberá qualquer confirmação se for bem-sucedido.
      
      ```bash
      su mssql
      ```
      
   1. Copie os arquivos do /var/opt/mssql/data diretório temporário. Você não receberá qualquer confirmação se for bem-sucedido.
      
      ```bash
      cp /var/opt/mssql/tmp/* /var/opt/mssql/data
      ```
      
   1. Verifique se que os arquivos estão lá.
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. Insira sair para não ser mssql 
      
   1. Insira sair para não ser a raiz
   
   1. Inicie o SQL Server. Se tudo o que foi copiado corretamente e a segurança aplicada corretamente, SQL Server deve aparecer como iniciado.
      
      ```bash
      sudo systemctl start mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. Para realizar mais testes, crie um banco de dados para garantir que as permissões são bem. O exemplo a seguir usa Transact-SQL; Você pode usar o SSMS.
      
      ![10_testcreatedb][2] 
      
   1. Interrompa o SQL Server e verifique se que ele está desligado. Se você pretende adicionar ou teste outros discos, não desligue do SQL Server até que essas são adicionadas e testadas.
      
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. Somente se terminar, desmonte o compartilhamento. Caso contrário, desmonte depois de concluir o teste/adicionando todos os discos adicionais.
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName > é o endereço IP ou nome do host SMB
      
      \<Nome de compartilhamento > é o nome do compartilhamento
      
      \<FolderMountedIn > é o nome da pasta em que o SMB é montado
      
5. Para outras coisas além de bancos de dados do sistema, como bancos de dados de usuário ou backups, siga estas etapas. Se apenas o local padrão, pule para a etapa 14.
   
   1. Opção a ser o superusuário. Você não receberá qualquer confirmação se for bem-sucedido.
      
      ```bash
      sudo -i
      ```
      
   1. Crie uma pasta que será usada pelo SQL Server. 
      
      ```bash
      mkdir <FolderName>
      ```
      
      \<Nome da pasta > é o nome da pasta. O caminho da pasta completo deve ser especificado se não está no local correto. O exemplo a seguir cria uma pasta chamada /var/opt/mssql/userdata.
      
      ```bash
      mkdir /var/opt/mssql/userdata
      ```
      
   1. Monte o compartilhamento SMB na pasta de dados do SQL Server. Você não receberá qualquer confirmação se for bem-sucedido. Este exemplo mostra a sintaxe para se conectar a um compartilhamento do Samba com base em SMB 3.0.
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName > é o nome do servidor com o compartilhamento SMB
      
      \<Nome de compartilhamento > é o nome do compartilhamento
      
      \<Nome da pasta > é o nome da pasta criada na última etapa  
      
      \<Nome de usuário > é o nome do usuário para acessar o compartilhamento
      
      \<Senha > é a senha do usuário
      
      \<mssqlUID > é o UID do usuário mssql
      
      \<mssqlGID > é o GID do usuário mssql.
      
   1. Verifique se a montagem foi bem-sucedida, emitindo montagem sem opções.
   
   1. Digite exit para não ser o superusuário.
   
   1. Para testar, crie um banco de dados nessa pasta. O exemplo a seguir usa o sqlcmd para criar um banco de dados, alternar o contexto para ele, verifique se os arquivos existem no nível de sistema operacional e, em seguida, exclui o local temporário. Você pode usar o SSMS.
   
   1. Desmontar o compartilhamento 
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName > é o endereço IP ou nome do host SMB
      
      \<Nome de compartilhamento > é o nome do compartilhamento
      
      \<FolderMountedIn > é o nome da pasta em que o SMB será montado.
   
1. Repita as etapas sobre os outros nós.

Agora você está pronto para configurar a FCI.

## <a name="next-steps"></a>Próximas etapas

[Configurar a instância de cluster de failover – SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 
