---
title: "Habilitar os pré-requisitos para FileTable | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FileTables [SQL Server], prerequisites
ms.assetid: 6286468c-9dc9-4eda-9961-071d2a36ebd6
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: da9c6ce47bf6ea04e47a04246fe5524dc1d3fddb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="enable-the-prerequisites-for-filetable"></a>Habilitar os pré-requisitos para FileTable
  Descreve como habilitar os pré-requisitos para criar e usar FileTables.  
  
##  <a name="EnablePrereq"></a> Habilitando os pré-requisitos para FileTable  
 Para habilitar os pré-requisitos para criar e usar FileTables, habilite os seguintes itens:  
  
-   **No nível de instância:**  
  
    -   [Habilitando o FILESTREAM no nível de instância](#BasicsFilestream)  
  
-   **No nível de banco de dados:**  
  
    -   [Fornecendo um grupo de arquivos FILESTREAM no nível de banco de dados](#filegroup)  
  
    -   [Habilitando o acesso não transacional em nível de banco de dados](#BasicsNTAccess)  
  
    -   [Especificando um diretório para FileTables no nível de banco de dados](#BasicsDirectory)  
  
##  <a name="BasicsFilestream"></a> Habilitando o FILESTREAM no nível de instância  
 As FileTables ampliam os recursos de FILESTREAM do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, você precisa habilitar o FILESTREAM para acesso de E/S de arquivo no nível do Windows e na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que possa criar e usar FileTables.  
  
###  <a name="HowToFilestream"></a> Como habilitar o FILESTREAM no nível de instância  
 Para obter informações sobre como habilitar o FILESTREAM, veja [Habilitar e configurar o FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md).  
  
 Quando você chama **sp_configure** para habilitar FILESTREAM no nível da instância, precisa definir a opção filestream_access_level como 2. Para obter mais informações, veja [Opção filestream access level de configuração de servidor](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md).  
  
###  <a name="firewall"></a> Como permitir o FILESTREAM através do Firewall  
 Para obter informações sobre como permitir o FILESTREAM através do firewall, consulte [Configure a Firewall for FILESTREAM Access](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md).  
  
##  <a name="filegroup"></a> Fornecendo um grupo de arquivos FILESTREAM no nível de banco de dados  
 Antes de você poder criar FileTables em um banco de dados, o banco de dados deve ter um grupo de arquivos FILESTREAM. Para obter mais informações sobre esses pré-requisitos, veja [Criar um banco de dados habilitado para FILESTREAM](../../relational-databases/blob/create-a-filestream-enabled-database.md).  
  
##  <a name="BasicsNTAccess"></a> Habilitando o acesso não transacional em nível de banco de dados  
 As FileTables permitem que os aplicativos do Windows obtenham um identificador de arquivo do Windows para dados de FILESTREAM sem precisar de uma transação. Para permitir esse acesso não transacional a arquivos armazenados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve especificar o nível desejado de acesso não transacional no nível de banco de dados para cada banco de dados que conterá FileTables.  
  
###  <a name="HowToCheckAccess"></a> Como verificar se o acesso não transacional está habilitado em bancos de dados  
 Consulte a exibição de catálogo [sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md) e verifique as colunas **non_transacted_access** e **non_transacted_access_desc**.  
  
```tsql  
SELECT DB_NAME(database_id), non_transacted_access, non_transacted_access_desc  
    FROM sys.database_filestream_options;  
GO  
```  
  
###  <a name="HowToNTAccess"></a> Como habilitar o acesso não transacional no nível de banco de dados  
 Os níveis disponíveis de acesso não transacional são FULL, READ_ONLY e OFF.  
  
 **Especificar o nível de acesso não transacional usando Transact-SQL**  
 -   Quando você **criar um novo banco de dados**, chame a instrução [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) com a opção **NON_TRANSACTED_ACCESS** de FILESTREAM.  
  
    ```tsql  
    CREATE DATABASE database_name  
        WITH FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' )  
    ```  
  
-   Ao **alterar um banco de dados existente**, chame a instrução [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md) com a opção FILESTREAM **NON_TRANSACTED_ACCESS**.  
  
    ```tsql  
    ALTER DATABASE database_name  
        SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' )  
    ```  
  
 **Especificar o nível de acesso não transacional usando o SQL Server Management Studio**  
 Você pode especificar o nível de acesso não transacional no campo **Acesso Não Transacionado a FILESTREAM** da página **Opções** da caixa de diálogo **Propriedades do Banco de dados** . Para obter mais informações sobre essa caixa de diálogo, veja [Propriedades de banco de dados &#40;Página Opções&#41;](../../relational-databases/databases/database-properties-options-page.md).  
  
##  <a name="BasicsDirectory"></a> Especificando um diretório para FileTables no nível de banco de dados  
 Quando você habilita o acesso não transacional a arquivos no nível de banco de dados, tem como opção fornecer um nome de diretório ao mesmo tempo usando a opção **DIRECTORY_NAME** . Se você não fornecer um nome de diretório ao habilitar o acesso não transacional, deverá fornecê-lo posteriormente para que possa criar FileTables no banco de dados.  
  
 Na hierarquia de pastas de FileTable, esse diretório em nível de banco de dados se torna o filho do nome de compartilhamento especificado para FILESTREAM no nível de instância, e o pai das FileTables criadas no banco de dados. Para obter mais informações, consulte [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
###  <a name="HowToDirectory"></a> Como especificar um diretório para FileTables no nível de banco de dados  
 O nome que você especifica deve estar exclusivo na instância para diretórios em nível de banco de dados.  
  
 **Especificar um diretório para FileTables usando Transact-SQL**  
 -   Quando você **criar um novo banco de dados**, chame a instrução [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) com a opção **DIRECTORY_NAME** de FILESTREAM.  
  
    ```tsql  
    CREATE DATABASE database_name  
        WITH FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   Ao **alterar um banco de dados existente**, chame a instrução [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md) com a opção FILESTREAM **DIRECTORY_NAME**. Quando você usa estas opções para alterar o nome do diretório, o banco de dados deve ser bloqueado de forma exclusiva, sem identificadores de arquivos abertos.  
  
    ```tsql  
    ALTER DATABASE database_name  
        SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   Ao **anexar um banco de dados**, chame a instrução [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) com a opção **FOR ATTACH** e com a opção FILESTREAM **DIRECTORY_NAME**.  
  
    ```tsql  
    CREATE DATABASE database_name  
        FOR ATTACH WITH FILESTREAM ( DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   Ao **restaurar um banco de dados**, chame a instrução [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md) com a opção FILESTREAM **DIRECTORY_NAME**.  
  
    ```tsql  
    RESTORE DATABASE database_name  
        WITH FILESTREAM ( DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
 **Especificar um diretório para FileTables usando o SQL Server Management Studio**  
 Você pode especificar um nome de diretório no campo **Nome do Diretório FILESTREAM** da página **Opções** da caixa de diálogo **Propriedades do Banco de dados** . Para obter mais informações sobre essa caixa de diálogo, veja [Propriedades de banco de dados &#40;Página Opções&#41;](../../relational-databases/databases/database-properties-options-page.md).  
  
###  <a name="viewnames"></a> Como exibir nomes de diretórios existentes para a instância  
 Para exibir a lista de nomes de diretórios existentes para a instância, veja a exibição de catálogo [sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md) e verifique a coluna **filestream_database_directory_name**.  
  
```tsql  
SELECT DB_NAME ( database_id ), directory_name  
    FROM sys.database_filestream_options;  
GO  
```  
  
###  <a name="ReqDirectory"></a> Requisitos e restrições para o diretório em nível de banco de dados  
  
-   Definir **DIRECTORY_NAME** é opcional quando você chama **CREATE DATABASE** ou **ALTER DATABASE**. Se você não especificar um valor para **DIRECTORY_NAME**, o nome de diretório permanecerá nulo. Entretanto, você só poderá criar FileTables no banco de dados quando especificar um valor para **DIRECTORY_NAME** no nível de banco de dados.  
  
-   O nome de diretório que você fornece deve atender aos requisitos do sistema de arquivos para um nome de diretório válido.  
  
-   Quando o banco de dados contém FileTables, não é possível definir **DIRECTORY_NAME** como um valor nulo.  
  
-   Quando você anexar ou restaurar um banco de dados, a operação falhará se o novo banco de dados tiver um valor para **DIRECTORY_NAME** já existente na instância de destino. Especifique um valor exclusivo para **DIRECTORY_NAME** quando chamar **CREATE DATABASE FOR ATTACH** ou **RESTORE DATABASE**.  
  
-   Quando você atualizar um banco de dados existente para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o valor de **DIRECTORY_NAME** será nulo.  
  
-   Quando você habilita ou desabilita o acesso não transacional no nível de banco de dados, a operação não verifica se o nome de diretório foi especificado ou se é exclusivo.  
  
-   Quando você remove um banco de dados que foi habilitado para FileTables, o diretório no nível de banco de dados e todas as estruturas de diretórios de todos os FileTables contidos nele serão removidos.  
  
  
