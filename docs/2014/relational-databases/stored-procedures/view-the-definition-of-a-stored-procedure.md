---
title: Exibir a definição de um procedimento armazenado| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], viewing
- definition of stored procedure
- viewing stored procedures
- displaying stored procedures
ms.assetid: 93318587-a0c5-4788-946f-3b5dc8372ea9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 333d4d9f0ab9feb5d5b5c4d0aa48fd584cef3143
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62856509"
---
# <a name="view-the-definition-of-a-stored-procedure"></a>Exibir a definição de um procedimento armazenado
    
##  <a name="Top"></a> Você pode exibir a definição de um procedimento armazenamento no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando as opções de menu do Pesquisador de Objetos ou no Editor de Consultas usando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Este tópico descreve como exibir a definição de procedimento no Pesquisador de Objetos e usando um procedimento armazenado do sistema, uma função de sistema e a exibição do catálogo de objetos no Editor de Consultas.  
  
-   **Antes de começar:**  [Segurança](#Security)  
  
-   **Para exibir a definição de um procedimento, usando:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Procedimento armazenado do sistema: `sp_helptext`  
 Requer associação à função **pública** . Definições de objeto de sistema são publicamente visíveis. A definição de objetos de usuário é visível para o proprietário do objeto ou aos que possuírem qualquer uma das seguintes permissões: ALTER, controle, TAKE OWNERSHIP ou VIEW DEFINITION.  
  
 Função do sistema: `OBJECT_DEFINITION`  
 Definições de objeto de sistema são publicamente visíveis. A definição de objetos de usuário é visível para o proprietário do objeto ou aos que possuírem qualquer uma das seguintes permissões: ALTER, controle, TAKE OWNERSHIP ou VIEW DEFINITION. Estas permissões são mantidas implicitamente por membros das funções fixas de banco de dados **db_owner**, **db_ddladmin**e **db_securityadmin** .  
  
 Exibição do catálogo de objetos: `sys.sql_modules`  
 A visibilidade dos metadados em exibições do catálogo está limitada aos protegíveis que pertencem a um usuário ou para os quais o usuário recebeu permissão. Para obter mais informações, consulte [Metadata Visibility Configuration](../security/metadata-visibility-configuration.md).  
  
##  <a name="Procedures"></a> Como exibir as definições de um procedimento armazenado  
 Você pode usar uma das seguintes opções:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para exibir a definição de um procedimento armazenado no Pesquisador de Objetos**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, expanda o banco de dados ao qual pertence o procedimento e expanda **Programação**.  
  
3.  Expandir **procedimentos armazenados**, o procedimento com o botão direito e, em seguida, clique em **Script de procedimento armazenado como**e, em seguida, clique em um dos seguintes: **Criar para**, **alterar para**, ou **descartar e criar para**.  
  
4.  Selecione **Janela do Editor de Nova Consulta**. Isso exibirá a definição de procedimento.  
  
###  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para exibir a definição de um procedimento no Editor de Consultas**  
  
 Procedimento armazenado do sistema: `sp_helptext`  
 1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra de ferramentas, clique em **Nova Consulta**.  
  
3.  Na janela de consulta, insira a instrução a seguir que usa o procedimento armazenado do sistema `sp_helptext`. Altere os nomes do banco de dados e do procedimento armazenado para fazer referência ao banco de dados e ao procedimento armazenado que você quer.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_helptext N'AdventureWorks2012.dbo.uspLogError';  
    ```  
  
 Função do sistema: `OBJECT_DEFINITION`  
 1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra de ferramentas, clique em **Nova Consulta**.  
  
3.  Na janela de consulta, insira as instruções a seguir que usam a função de sistema `OBJECT_DEFINITION`. Altere os nomes do banco de dados e do procedimento armazenado para fazer referência ao banco de dados e ao procedimento armazenado que você quer.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_DEFINITION (OBJECT_ID(N'AdventureWorks2012.dbo.uspLogError'));  
    ```  
  
 Exibição do catálogo de objetos: `sys.sql_modules`  
 1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra de ferramentas, clique em **Nova Consulta**.  
  
3.  Na janela de consulta, insira as instruções a seguir que usam a exibição de catálogo `sys.sql_modules`. Altere os nomes do banco de dados e do procedimento armazenado para fazer referência ao banco de dados e ao procedimento armazenado que você quer.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT definition  
    FROM sys.sql_modules  
    WHERE object_id = (OBJECT_ID(N'AdventureWorks2012.dbo.uspLogError'));  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Criar um procedimento armazenado](create-a-stored-procedure.md)   
 [Modificar um procedimento armazenado](modify-a-stored-procedure.md)   
 [Excluir um procedimento armazenado](delete-a-stored-procedure.md)   
 [Renomear um procedimento armazenado](rename-a-stored-procedure.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](/sql/t-sql/functions/object-definition-transact-sql)   
 [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)   
 [sp_helptext &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptext-transact-sql)   
 [OBJECT_ID &#40;Transact-SQL&#41;](/sql/t-sql/functions/object-id-transact-sql)  
  
  
