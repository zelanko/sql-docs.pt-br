---
title: Criar uma especificação de auditoria de banco de dados e de servidor
description: Saiba como criar uma especificação de auditoria do SQL Server e do banco de dados com o SQL Server Management Studio ou o T-SQL (Transact-SQL).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.sqlaudit.dbaudit.general.f1
helpviewer_keywords:
- audits [SQL Server], creating database specification
- database audit [SQL Server]
ms.assetid: 26ee85de-6e97-4318-b526-900924d96e62
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 55b848cd43e157a9a75670a24aea645c3279f7ea
ms.sourcegitcommit: bfb5e79586fd08d8e48e9df0e9c76d1f6c2004e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/29/2020
ms.locfileid: "82262070"
---
# <a name="create-a-server-audit-and-database-audit-specification"></a>Criar uma especificação de auditoria de banco de dados e de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este artigo descreve como criar uma especificação de auditoria de servidor e de banco de dados no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Auditar uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] envolve rastrear e registrar em log os eventos que ocorrem no sistema. O objeto de *Auditoria do SQL Server* coleta uma instância única de ações no nível do servidor ou do banco de dados e grupos de ações a serem monitoradas. A auditoria está no nível de instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Você pode ter várias auditorias por instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . O objeto *Especificação de Auditoria de Banco de Dados* pertence a uma auditoria. É possível criar uma especificação da auditoria de banco de dados por banco de dados do SQL Server por auditoria. Para obter mais informações, confira [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 ##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
 As especificações de auditoria de banco de dados são objetos não protegidos que residem em um determinado banco de dados. Quando uma especificação de auditoria de banco de dados é criada, ela fica em um estado desabilitado.  
  
 Quando estiver criando ou modificando uma especificação de auditoria de banco de dados em um banco de dados de usuário, não inclua ações de auditoria em objetos do escopo de servidor, como as exibições do sistema. Se forem incluídos objetos de escopo do servidor, a auditoria será criada. No entanto, os objetos de escopo do servidor não serão incluídos e nenhum erro será retornado. Para auditar objetos de escopo do servidor, use uma especificação de auditoria de banco de dados no banco de dados mestre.  
  
 As especificações de auditoria de banco de dados residem no banco de dados quando são criadas, com exceção do banco de dados do sistema **TempDB**.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
  
-   Os usuários com a permissão ALTER ANY DATABASE AUDIT podem criar especificações de auditoria de banco de dados e associá-las a auditorias.  
  
-   Depois que uma especificação de auditoria de banco de dados é criada, entidades com as permissões CONTROL SERVER ou ALTER ANY DATABASE AUDIT podem exibi-la. A conta sysadmin também pode exibi-la.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-server-audit"></a>Para criar uma auditoria de servidor  
  
1.  No Pesquisador de Objetos, expanda a pasta **Segurança** .  
  
2.  Clique com o botão direito do mouse na pasta **Auditorias** e selecione **Nova Auditoria**. Para obter mais informações, confira [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md).  
  
3.  Quando terminar de selecionar as opções, selecione **OK**.  

#### <a name="to-create-a-database-level-audit-specification"></a>Para criar uma especificação de auditoria no nível de banco de dados  
  
1.  No Pesquisador de Objetos, expanda o banco de dados no qual deseja criar a especificação de auditoria.  
  
2.  Expanda a pasta **Segurança** .  
  
3.  Clique com o botão direito do mouse na pasta **Especificações de Auditoria do Banco de Dados** e selecione **Nova Especificação de Auditoria do Banco de Dados**.  
  
     Estas opções estão disponíveis na caixa de diálogo **Criar Especificação de Auditoria de Banco de Dados**:  
  
     **Nome**  
     O nome da especificação de auditoria de banco de dados. Um nome é gerado automaticamente quando você cria uma especificação de auditoria de servidor. O nome é editável.  
  
     **Auditoria**  
     O nome de um objeto de auditoria de servidor existente. Digite o nome da auditoria ou selecione-o na lista.  
  
     **Tipo de Ação de Auditoria**  
     Especifica os grupos de ação de auditoria no nível de banco de dados e as ações de auditoria a capturar. Para obter uma lista dos grupos de ação de auditoria no nível de banco de dados, ações de auditoria e uma descrição dos eventos que eles contêm, confira [Ações e grupos de ações de auditoria do SQL Server](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
     **Esquema de Objeto**  
     Exibe o esquema para **Object Name**especificado.  
  
     **Object Name**  
     Nome do objeto a ser auditado. Esta opção está disponível somente para ações de auditoria. Ela não se aplica a grupos de auditoria.  
  
     **Reticências (...)**  
     Abre a caixa de diálogo **Selecionar Objetos** para que você possa procurar e selecionar um objeto disponível, com base no **Tipo de Ação de Auditoria** especificado.  
  
     **Nome Principal**  
     A conta para filtrar a auditoria para o objeto que está sendo auditado.  
  
     **Reticências (...)**  
     Abre a caixa de diálogo **Selecionar Objetos** para que você possa procurar e selecionar um objeto disponível, com base no **Nome do Objeto** especificado.  
  
4.  Quando terminar de selecionar as opções, selecione **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-server-audit"></a>Para criar uma auditoria de servidor  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, selecione **Nova Consulta**.  
  
3.  Cole o exemplo a seguir na janela de consulta e selecione **Executar**.  
  
    ```  
    USE master ;  
    GO  
    -- Create the server audit.   
    CREATE SERVER AUDIT Payrole_Security_Audit  
        TO FILE ( FILEPATH =   
    'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA' ) ;   
    GO  
    -- Enable the server audit.   
    ALTER SERVER AUDIT Payrole_Security_Audit   
    WITH (STATE = ON) ;  
    ```  
  
#### <a name="to-create-a-database-level-audit-specification"></a>Para criar uma especificação de auditoria no nível de banco de dados  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, selecione **Nova Consulta**.  
  
3.  Cole o exemplo a seguir na janela de consulta e selecione **Executar**. Este exemplo cria uma especificação de auditoria de banco de dados chamada `Audit_Pay_Tables`. Ela audita as instruções SELECT e INSERT pelo usuário `dbo` para a tabela `HumanResources.EmployeePayHistory`, com base na auditoria do servidor definida na seção anterior.  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    -- Create the database audit specification.   
    CREATE DATABASE AUDIT SPECIFICATION Audit_Pay_Tables  
    FOR SERVER AUDIT Payrole_Security_Audit  
    ADD (SELECT , INSERT  
         ON HumanResources.EmployeePayHistory BY dbo )   
    WITH (STATE = ON) ;   
    GO  
  
    ```  
  
 Para obter mais informações, veja [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md) e [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-audit-specification-transact-sql.md).  
  
  
