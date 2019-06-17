---
title: Habilitar índices e restrições | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexes [SQL Server], enabling
- nonclustered indexes [SQL Server], enabling a disabled index
- index enabling [SQL Server]
- disabled indexes [SQL Server], how to enable
- constraints [SQL Server], enabling
- clustered indexes, enabling disabled indexes
ms.assetid: c55c8865-322e-4ab0-ba04-ea1f56735353
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7d68f329aecdd1284bac311db4139470bba55e41
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162385"
---
# <a name="enable-indexes-and-constraints"></a>Habilitar índices e restrições
  Este tópico descreve como habilitar um índice desabilitado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Depois que um índice for desabilitado, ele permanecerá em estado desabilitado até que seja recriado ou descartado  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para habilitar um índice desabilitado, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Depois da reconstrução do índice, qualquer restrição que tiver sido desabilitada devido à desabilitação do índice deverá ser habilitada manualmente. As restrições PRIMARY KEY e UNIQUE são habilitadas reconstruindo o índice associado. Esse índice deve ser reconstruído (habilitado) antes de você poder habilitar restrições FOREIGN KEY que fazem referência à restrição PRIMARY KEY ou UNIQUE. Restrições FOREIGN KEY são habilitadas usando a instrução ALTER TABLE CHECK CONSTRAINT.  
  
-   A recriação de um índice clusterizado desabilitado não pode ser efetuada quando a opção ONLINE está definida como ON.  
  
-   Quando o índice clusterizado é habilitado ou desabilitado e o índice não clusterizado é desabilitado, a ação do índice clusterizado tem os seguintes resultados no índice não clusterizado desabilitado.  
  
    |Ação de índice clusterizado|Índice não clusterizado desabilitado...|  
    |----------------------------|-----------------------------------|  
    |ALTER INDEX REBUILD.|Permanece desabilitado.|  
    |ALTER INDEX ALL REBUILD.|É reconstruído e habilitado.|  
    |DROP INDEX.|Permanece desabilitado.|  
    |CREATE INDEX WITH DROP_EXISTING.|Permanece desabilitado.|  
  
     A criação de um novo índice clusterizado se comporta da mesma forma que ALTER INDEX ALL REBUILD.  
  
-   Ações permitidas em índices não clusterizados associados a um índice clusterizado dependem do estado, se desabilitado ou habilitado, de ambos os tipos de índice. A tabela a seguir resume as ações permitidas em índices não clusterizados.  
  
    |Ação de índice não clusterizado|Quando os índices clusterizados e não clusterizados estão desabilitados.|Quando o índice clusterizado está habilitado e o índice não clusterizado está em um dos estados.|  
    |-------------------------------|--------------------------------------------------------------------|----------------------------------------------------------------------------------------|  
    |ALTER INDEX REBUILD.|A ação falha.|A ação tem êxito.|  
    |DROP INDEX.|A ação tem êxito.|A ação tem êxito.|  
    |CREATE INDEX WITH DROP_EXISTING.|A ação falha.|A ação tem êxito.|  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na tabela ou exibição. Se estiver usando o DBCC DBREINDEX, o usuário deverá ter a tabela ou ser membro da função de servidor fixa **sysadmin** ou das funções de banco de dados fixas **db_ddladmin** e **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-enable-a-disabled-index"></a>Para habilitar um índice desabilitado  
  
1.  No Pesquisador de Objetos, clique no sinal de adição para expandir o banco de dados que contém a tabela na qual você deseja habilitar um índice.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela na qual você deseja habilitar um índice.  
  
4.  Clique no sinal de adição para expandir a pasta **Índices** .  
  
5.  Clique com o botão direito do mouse no índice a ser habilitado e selecione **Recriar**.  
  
6.  Na caixa de diálogo **Recriar Índices** , verifique se o índice correto está na grade **Índices a serem recriados** e clique em **OK**.  
  
#### <a name="to-enable-all-indexes-on-a-table"></a>Para habilitar todos os índices de uma tabela  
  
1.  No Pesquisador de Objetos, clique no sinal de adição para expandir o banco de dados que contém a tabela na qual você deseja habilitar os índices.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela na qual você deseja habilitar os índices.  
  
4.  Clique com o botão direito do mouse na pasta **Índices** e selecione **Recriar Tudo**.  
  
5.  Na caixa de diálogo **Recriar Índices** , verifique se os índices corretos estão na grade **Índices a serem recriados** e clique em **OK**. Para remover um índice da grade **Índices a serem recriados** , selecione o índice e pressione a tecla Delete.  
  
 As seguintes informações estão disponíveis na caixa de diálogo **Recriar Índices** :  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-enable-a-disabled-index-using-alter-index"></a>Para habilitar um índice desabilitado usando ALTER INDEX  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Enables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table.  
  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    REBUILD;   
    GO  
    ```  
  
#### <a name="to-enable-a-disabled-index-using-create-index"></a>Para habilitar um índice desabilitado usando CREATE INDEX  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- re-creates the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    -- using the OrganizationLevel and OrganizationNode columns  
    -- and then deletes the existing IX_Employee_OrganizationLevel_OrganizationNode index  
    CREATE INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
       (OrganizationLevel, OrganizationNode)  
    WITH (DROP_EXISTING = ON);  
    GO  
    ```  
  
#### <a name="to-enable-a-disabled-index-using-dbcc-dbreindex"></a>Para habilitar um índice desabilitado usando DBCC DBREINDEX  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- enables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    DBCC DBREINDEX ("HumanResources.Employee", IX_Employee_OrganizationLevel_OrganizationNode);  
    GO  
    ```  
  
#### <a name="to-enable-all-indexes-on-a-table-using-alter-index"></a>Para habilitar todos os índices em uma tabela usando ALTER INDEX  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- enables all indexes  
    -- on the HumanResources.Employee table  
    ALTER INDEX ALL ON HumanResources.Employee  
    REBUILD;  
    GO  
    ```  
  
#### <a name="to-enable-all-indexes-on-a-table-using-dbcc-dbreindex"></a>Para habilitar todos os índices em uma tabela usando DBCC DBREINDEX  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- enables all indexes  
    -- on the HumanResources.Employee table  
    DBCC DBREINDEX ("HumanResources.Employee", " ");  
    GO  
    ```  
  
 Para obter mais informações, veja [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql), [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql) e [DBCC DBREINDEX &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql).  
  
  
