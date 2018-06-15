---
title: Configurar o failover cluster instância armazenamento SMB - SQL Server no Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: b762740be742aa2d716b9d354c26fe87bb170732
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34322967"
---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>Configurar a instância de cluster de failover - SMB - SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo explica como configurar o armazenamento SMB para uma instância de cluster de failover (FCI) no Linux. 
 
No mundo não Windows, SMB é geralmente conhecido para como um arquivo de sistema CIFS (Common Internet) compartilhar e implementado por meio do Samba. No mundo do Windows, acessar um compartilhamento SMB é feito desta forma: \\SERVERNAME\SHARENAME. Para instalações do SQL Server com base em Linux, o compartilhamento SMB deve ser montado como uma pasta.

## <a name="important-source-and-server-information"></a>Informações importantes de origem e de servidor

Aqui estão algumas dicas e observações para usar com êxito o SMB:
- O compartilhamento SMB pode estar no Windows, Linux, ou mesmo de um dispositivo como desde que ela está usando SMB 3.0 ou superior. Para obter mais informações sobre o Samba e o SMB 3.0, consulte [SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0) para ver se sua implementação Samba é compatível com SMB 3.0.
- O compartilhamento SMB deve estar altamente disponível.
- Segurança deve ser configurada corretamente no compartilhamento SMB. Abaixo está um exemplo de /etc/samba/smb.conf, onde SQLData1 é o nome do compartilhamento.

![smbsource 05][1]

## <a name="instructions"></a>Instruções

1.  Escolha um dos servidores que participarão na configuração de FCI. Não importa qual delas.

2.  Obter informações sobre o usuário mssql.

    ```bash
    sudo id mssql
    ```
    
    Observe o uid, gid e grupos. 

3. Execute `sudo smbclient -L //NameOrIP/ShareName -U User`.

    \<NameOrIP > é o nome DNS ou endereço IP do servidor que hospeda o compartilhamento SMB.

    \<Nome de compartilhamento > é o nome do compartilhamento SMB. 

4. Para o sistema de bancos de dados ou qualquer coisa armazenada no local de dados padrão siga estas etapas. Caso contrário, pule para a etapa 5. 

   *    Certifique-se de que o SQL Server está interrompido no servidor que você está trabalhando.
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    Opção totalmente para ser o superusuário. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    sudo -i
    ```

   *    Alternar para ser o usuário mssql. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    su mssql
    ```

   *    Crie um diretório temporário para armazenar dados do SQL Server e os arquivos de log. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    mkdir <TempDir>
    ```

    <TempDir> é o nome da pasta. O exemplo a seguir cria uma pasta chamada /var/opt/mssql/tmp.

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   *    Copie os arquivos de log e de dados do SQL Server para o diretório temporário. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > é o nome da pasta da etapa anterior.
    
   *    Verifique se os arquivos no diretório.

    ```bash
    ls <TempDir>
    ```

    \<TempDir > é o nome da pasta da etapa d.
    
   *    Exclua os arquivos do diretório de dados do SQL Server existente. Você não receberá nenhuma confirmação se for bem-sucedido.
 
    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   *    Verifique se que os arquivos foram excluídos. 

    ```bash
    ls /var/opt/mssql/data
    ```
 
   *    Tipo de saída para alternar novamente para o usuário raiz.

   *    Monte o compartilhamento SMB na pasta de dados do SQL Server. Você não receberá nenhuma confirmação se for bem-sucedido. Este exemplo mostra a sintaxe para se conectar a um compartilhamento com o Windows Server SMB 3.0.

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
 
   *    Verifique se a montagem foi bem-sucedida, emitindo montagem sem opções.

    ```bash
    mount
    ```
 
   *    Alterne para o usuário mssql. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    su mssql
    ```

   *    Copie os arquivos do /var/opt/mssql/data diretório temporário. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssql/data
    ```

   *    Verifique se que os arquivos estão lá.

    ```bash
    ls /var/opt/mssql/data
    ```

   *    Digite Sair para não ser mssql 

   *    Digite Sair para não ser raiz

   *    Inicie o SQL Server. Se tudo foi copiado corretamente e segurança aplicada corretamente, do SQL Server deve mostrar é iniciado.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
 
   *    Para testar adicional, crie um banco de dados para garantir que as permissões são permitidas. O exemplo a seguir usa Transact-SQL; Você pode usar o SSMS.

    ![10_testcreatedb][2] 
  
   *    Interrompa o SQL Server e verifique se que ele está desligado. Se você pretende ser adicionando ou outros discos de teste, não desligue do SQL Server até que essas são adicionadas e testadas.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    Somente for concluída, desmonte o compartilhamento. Caso contrário, desmonte-o depois de concluir o teste/adicionar discos adicionais.

    ```bash
    sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
    ```

    \<IPAddressOrServerName > é o endereço IP ou nome do host SMB

    \<Nome de compartilhamento > é o nome do compartilhamento
    
    \<FolderMountedIn > é o nome da pasta em que o SMB está montado

5.  Para tarefas diferentes bancos de dados do sistema, como bancos de dados de usuário ou backups, siga estas etapas. Se apenas usando o local padrão, vá para a etapa 14.
    
   *    Alternar para ser o superusuário. Você não receberá nenhuma confirmação se for bem-sucedido.

    ```bash
    sudo -i
    ```
    
   *    Crie uma pasta que será usada pelo SQL Server. 

    ```bash
    mkdir <FolderName>
    ```

    \<Nome da pasta > é o nome da pasta. Caminho completo da pasta deve ser especificado se não está no local correto. O exemplo a seguir cria uma pasta chamada /var/opt/mssql/userdata.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    Monte o compartilhamento SMB na pasta de dados do SQL Server. Você não receberá nenhuma confirmação se for bem-sucedido. Este exemplo mostra a sintaxe para se conectar a um compartilhamento com base em Samba SMB 3.0.

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
 
   * Verifique se a montagem foi bem-sucedida, emitindo montagem sem opções.
 
   * Tipo de saída não seja o superusuário.

   * Para testar, crie um banco de dados nessa pasta. O exemplo a seguir usa o sqlcmd para criar um banco de dados, alterne o contexto para ele, verifique se os arquivos existem no nível do sistema operacional e, em seguida, exclui o local temporário. Você pode usar o SSMS.
 
   * Desmontar o compartilhamento 

    ```bash
    sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
    ```
    
    \<IPAddressOrServerName > é o endereço IP ou nome do host SMB
 
    \<Nome de compartilhamento > é o nome do compartilhamento
 
    \<FolderMountedIn > é o nome da pasta em que o SMB está montado.
 
6.  Repita as etapas nos outros nós.

Agora você está pronto para configurar a FCI.

## <a name="next-steps"></a>Próximas etapas

[Configurar a instância de cluster de failover - SQL Server no Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 
