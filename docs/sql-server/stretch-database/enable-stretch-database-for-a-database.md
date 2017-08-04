---
title: Habilitar o Stretch Database para um banco de dados | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 08/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, enabling database
- enabling database for Stretch Database
ms.assetid: 37854256-8c99-4566-a552-432e3ea7c6da
caps.latest.revision: 70
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 189aef1d316d4e8569a48a413ec72cfbc6a6673c
ms.contentlocale: pt-br
ms.lasthandoff: 07/29/2017

---
# <a name="enable-stretch-database-for-a-database"></a>Enable Stretch Database for a database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Para configurar um banco de dados para o Stretch Database, selecione **Tarefas | Stretch | Habilitar** para um banco de dados no SQL Server Management Studio a fim de abrir o assistente **Habilitar Banco de Dados para Stretch**. Você também pode usar o Transact-SQL de modo a habilitar o Stretch Database para um banco de dados.  
  
 Se você selecionar **Tarefas | Stretch | Habilitar** para uma tabela individual e ainda não tiver habilitado o banco de dados para o Stretch Database, o assistente vai configurar o banco de dados para o Stretch Database e permitirá que você selecione tabelas como parte do processo. Siga as etapas deste tópico em vez das etapas em [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md).  
  
 Habilitar o Stretch Database em um banco de dados ou uma tabela exige permissões db_owner. Habilitar o Stretch Database em um banco de dados também exige permissões CONTROL DATABASE.  

 >   [!NOTE]
 > Mais tarde, se você desabilitar o Stretch Database, lembre-se de que desabilitar uma tabela ou um banco de dados do Stretch Database não excluirá o objeto remoto. Se você quiser excluir a tabela remota ou o banco de dados remoto, descarte-o(a) usando o Portal de Gerenciamento do Azure. Os objetos remotos continuam incorrendo em custos do Azure até que você os exclua manualmente. 
 
## <a name="before-you-get-started"></a>Antes de começar  
  
-   Antes de configurar um banco de dados para o Stretch, é recomendável executar o Supervisor do Stretch Database para identificar bancos de dados e tabelas qualificados para o Stretch. O Supervisor do Stretch Database também identifica problemas de bloqueio. Para obter mais informações, veja [Identificar bancos de dados e tabelas para o Stretch Database executando o supervisor do Stretch Database](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md).  
  
-   Leia [Limitações do Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md).  
  
-   O Stretch Database migra dados para o Azure. Portanto, você precisa ter uma conta do Azure e uma assinatura para cobrança. Para obter uma conta do Azure, [clique aqui](http://azure.microsoft.com/en-us/pricing/free-trial/).  
  
-   Ter as informações de conexão e o logon necessárias para criar um novo servidor do Azure ou para selecionar um servidor do Azure existente.  
  
##  <a name="EnableTSQLServer"></a> Pré-requisito: habilitar Stretch Database no servidor  
 Para que seja possível habilitar o Stretch Database em um banco de dados ou em uma tabela, você precisa habilitá-lo no servidor local. Essa operação requer permissões sysadmin ou serveradmin.  
  
-   Se você tiver as permissões administrativas necessárias, o assistente **Habilitar o Banco de Dados para Stretch** vai configurar o servidor para o Stretch.  
  
-   Se você não tiver as permissões necessárias, um administrador deverá habilitar a opção manualmente executando **sp_configure** antes de executar o assistente ou um administrador terá que executar o assistente.  
  
 Para habilitar o Stretch Database no servidor manualmente, execute **sp_configure** e ative a opção **remover arquivo de dados** . O exemplo a seguir habilita a opção **remote data archive** definindo seu valor para 1.  
  
```  
EXEC sp_configure 'remote data archive' , '1';  
GO

RECONFIGURE;  
GO  
```  
  
 Para obter mais informações, consulte [Configurar a Opção de Configuração do Servidor de arquivo de dados remotos](../../database-engine/configure-windows/configure-the-remote-data-archive-server-configuration-option.md) e [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
##  <a name="Wizard"></a> Usar o assistente para habilitar o Stretch Database em um banco de dados  
 Para obter informações sobre o Assistente Habilitar o Banco de Dados para Stretch, incluindo as informações que você tem que inserir e as escolhas que tem que fazer, confira [Comece executando o Assistente para habilitar o banco de dados para Stretch](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md).  
  
##  <a name="EnableTSQLDatabase"></a> Usar o Transact-SQL para habilitar o Stretch Database em um banco de dados  
 Para que seja possível habilitar o Stretch Database em tabelas individuais, você precisa habilitá-lo no banco de dados.  
  
 Habilitar o Stretch Database em um banco de dados ou uma tabela exige permissões db_owner. Habilitar o Stretch Database em um banco de dados também exige permissões CONTROL DATABASE.  
  
1.  Antes de começar, escolha um servidor do Azure existente para os dados que o Stretch Database migra, ou crie um novo servidor do Azure.  
  
2.  No servidor do Azure, crie uma regra de firewall com o intervalo de endereços IP do SQL Server que permita ao SQL Server se comunicar com o servidor remoto.  

    Você pode encontrar facilmente os valores necessários e criar a regra de firewall ao tentar se conectar ao servidor do Azure no Pesquisador de Objetos do SSMS (SQL Server Management Studio). O SSMS o ajuda a criar a regra, abrindo a caixa de diálogo a seguir, que já inclui os valores de endereços IP necessários.
    
    ![Regra de firewall para o Stretch](../../sql-server/stretch-database/media/firewall-rule-for-stretch.png)
  
3.  Para configurar um banco de dados do SQL Server para o Stretch Database, o banco de dados deve ter uma chave mestra de banco de dados. A chave mestra de banco de dados protege as credenciais usadas pelo Stretch Database para se conectar ao banco de dados remoto. Aqui está um exemplo que cria uma nova chave mestra de banco de dados.  
  
    ```tsql  
    USE <database>; 
    GO  
  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD='<password>'; 
    GO
    ```  
    Para obter mais informações sobre a chave mestra do banco de dados, veja [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) e [Criar uma chave mestra de banco de dados](../../relational-databases/security/encryption/create-a-database-master-key.md).
    
4.  Quando você configura um banco de dados para o Stretch Database, é preciso fornecer uma credencial para o Stretch Database usar na comunicação entre o SQL Server local e o servidor remoto do Azure. Você tem duas opções.  
  
    -   É possível fornecer uma credencial administrativa.  
  
        -   Se você habilitar o Stretch Database executando o assistente, será possível criar a credencial nesse momento.  
  
        -   Se você planeja habilitar o Stretch Database executando **ALTER DATABASE**, será preciso criar a credencial manualmente antes de executar **ALTER DATABASE** para habilitar o Stretch Database. 
        
        Aqui está um exemplo que cria uma nova credencial.
  
        ```tsql  
        CREATE DATABASE SCOPED CREDENTIAL <db_scoped_credential_name>  
            WITH IDENTITY = '<identity>' , SECRET = '<secret>' ;
        GO   
        ```  

         Para obter mais informações sobre as credenciais, consulte [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md). A criação da credencial exige permissões ALTER ANY CREDENTIAL.  

    -   Você pode usar uma conta de serviço federado para o SQL Server se comunicar com o servidor remoto do Azure quando todas as condições a seguir forem verdadeiras.  
  
        -   A conta do serviço na qual a instância do SQL Server está sendo executada é uma conta de domínio.  
  
        -   A conta de domínio pertence a um domínio cujo Active Directory é federado com o Azure Active Directory.  
  
        -   O servidor remoto do Azure está configurado para permitir a autenticação do Azure Active Directory.  
  
        -   A conta de serviço na qual a instância do SQL Server está sendo executada deve ser configurada como uma conta dbmanager ou sysadmin no servidor remoto do Azure.  
  
5.  Para configurar um banco de dados para o Stretch Database, execute o comando ALTER DATABASE.  
  
    1.  Para o argumento SERVER, forneça o nome de um servidor existente do Azure, incluindo a parte `.database.windows.net` do nome; por exemplo, `MyStretchDatabaseServer.database.windows.net`.  
  
    2.  Forneça uma credencial de administrador existente com o argumento CREDENTIAL ou especifique FEDERATED_SERVICE_ACCOUNT = ON. O exemplo a seguir fornece uma credencial existente.  
  
    ```tsql  
    ALTER DATABASE <database name>  
        SET REMOTE_DATA_ARCHIVE = ON  
            (  
                SERVER = '<server_name>' ,  
                CREDENTIAL = <db_scoped_credential_name>  
            ) ;  
    GO
    ```  
  
## <a name="next-steps"></a>Próximas etapas  
-   [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) para habilitar outras tabelas.  
  
-   [Monitorar e solucionar problemas de migração de dados &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) para ver o status da migração de dados.  
  
-   [Pausar e retomar a migração de dados &#40;Stretch Database&#41;](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
-   [Gerenciar e solucionar problemas no Stretch Database](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
-   [Fazer backup de bancos de dados habilitados para Stretch](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
  
-   [Restaurar bancos de dados habilitados para Stretch](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
## <a name="see-also"></a>Consulte também  
 [Identificar bancos de dados e tabelas para o Stretch Database executando o supervisor do Stretch Database](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  

