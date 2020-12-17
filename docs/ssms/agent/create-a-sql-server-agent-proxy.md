---
description: Criar um proxy do SQL Server Agent
title: Criar um proxy do SQL Server Agent
ms.custom: seo-lt-2019
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- proxies [SQL Server Agent], creating
ms.assetid: 142e0c55-a8b9-4669-be49-b9dc602d5988
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 5c1d585b1d769c35f63cd608c266ee510613a9bf
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464427"
---
# <a name="create-a-sql-server-agent-proxy"></a>Criar um proxy do SQL Server Agent
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Este tópico descreve como criar um proxy do SQL Server Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
Uma conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent define o contexto de segurança no qual uma etapa de trabalho pode ser executada. Cada proxy corresponde a uma credencial de segurança. Para definir as permissões para uma etapa de trabalho em particular, crie um proxy com as permissões necessárias para um subsistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e atribua-o à etapa de trabalho.  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitações e Restrições  
  
-   Primeiro, é necessário criar uma credencial antes de criar um proxy, caso não haja nenhuma disponível.  
  
-   Os proxies do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usam credenciais para armazenar informações sobre as contas de usuário do Windows. O usuário especificado na credencial deve ter permissão para "Acessar esse computador pela rede" (SeNetworkLogonRight) no computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent verifica o acesso a subsistemas de um proxy e fornece acesso ao proxy sempre que a etapa de trabalho é executada. Se o proxy já não tiver acesso ao subsistema, a etapa de trabalho falhará. Caso contrário, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent representará o usuário especificado no proxy e executará a etapa de trabalho.  
  
-   A criação de um proxy não altera as permissões do usuário especificado na credencial do proxy. Por exemplo, você pode criar um proxy para um usuário que não tem permissão de se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nesse caso, as etapas de trabalho que usarem esse proxy não conseguirão se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Se o logon do usuário tiver acesso ao proxy ou se o usuário pertencer a alguma função com acesso ao proxy, ele poderá utilizá-lo em uma etapa de trabalho.  
  
### <a name="security"></a><a name="Security"></a>Segurança  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissões  
  
-   Apenas membros da função de servidor fixa **sysadmin** têm permissão para criar, modificar ou excluir contas proxy. Usuários que não sejam membros da função de servidor fixa **sysadmin** devem ser adicionados a uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** para poderem usar proxies: **SQLAgentUserRole**, **SQLAgentReaderRole** ou **SQLAgentOperatorRole**.  
  
-   Requer a permissão **ALTER ANY CREDENTIAL** para criar uma credencial além do proxy.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-sql-server-agent-proxy"></a>Para criar um proxy do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja criar um proxy no SQL Server Agent.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse na pasta **Proxies** e selecione **Novo Proxy**.  
  
4.  Na caixa de diálogo **Nova Conta Proxy** , na página **Geral** , digite o nome da nova conta proxy na caixa **Nome do proxy** .  
  
5.  Na caixa de diálogo **Nome da credencial** , digite o nome da credencial de segurança que a conta proxy usará.  
  
6.  Na caixa **Descrição** , digite uma descrição da conta proxy.  
  
7.  Em **Ativo nos seguintes subsistemas**, selecione o subsistema ou os subsistemas apropriados para esse proxy.  
  
8.  Na página **Entidades** , adicione ou remova logons ou funções para conceder ou remover acesso à conta proxy.  
  
9. Quando terminar, clique em **OK**.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-create-a-sql-server-agent-proxy"></a>Para criar um proxy do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- creates credential CatalogApplicationCredential  
    USE msdb ;  
    GO  
    CREATE CREDENTIAL CatalogApplicationCredential WITH IDENTITY = 'REDMOND/TestUser',   
        SECRET = 'G3$1o)lkJ8HNd!';  
    GO  
    -- creates proxy "Catalog application proxy" and assigns
    -- the credential 'CatalogApplicationCredential' to it.  
    EXEC dbo.sp_add_proxy  
        @proxy_name = 'Catalog application proxy',  
        @enabled = 1,  
        @description = 'Maintenance tasks on catalog application.',  
        @credential_name = 'CatalogApplicationCredential' ;  
    GO  
    -- grants the proxy "Catalog application proxy" access to 
    -- the ActiveX Scripting subsystem.  
    EXEC dbo.sp_grant_proxy_to_subsystem  
        @proxy_name = N'Catalog application proxy',  
        @subsystem_id = 2 ;  
    GO  
    ```  
  
Para obter mais informações, consulte:  
  
-   [CREATE CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-credential-transact-sql.md)  
  
-   [sp_add_proxy (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)  
  
-   [sp_grant_proxy_to_subsystem (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
