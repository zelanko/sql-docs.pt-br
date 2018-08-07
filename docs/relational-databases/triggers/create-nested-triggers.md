---
title: Criar gatilhos aninhados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- recursive DML triggers [SQL Server]
- DML triggers, nested
- triggers [SQL Server], nested
- direct recursion [SQL Server]
- triggers [SQL Server], recursive
- DML triggers, recursive
- RECURSIVE_TRIGGERS option
- indirect recursion [SQL Server]
- nested DML triggers
ms.assetid: cd522dda-b4ab-41b8-82b0-02445bdba7af
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 90d8fab908859ececf171801bba238909470272e
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39553246"
---
# <a name="create-nested-triggers"></a>Criar gatilhos aninhados
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Os gatilhos DML e DDL são aninhados quando um gatilho executa uma ação que inicia outro gatilho. Essas ações podem iniciar outros gatilhos, e assim por diante. Os gatilhos DML e DDL podem ser aninhados em até 32 níveis. Você pode controlar se os gatilhos AFTER podem ser aninhados pela opção de configuração do servidor **nested triggers** . Os gatilhos INSTEAD OF (apenas gatilhos DML podem ser gatilhos INSTEAD OF) podem ser aninhados, independentemente dessa configuração.  
  
> [!NOTE]  
>  Qualquer referência a um código gerenciado de um gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)] conta como um nível em relação ao limite de 32 níveis de aninhamento. Os métodos invocados a partir do código gerenciado não são contados em relação a esse limite.  
  
 Se gatilhos aninhados forem permitidos e um gatilho na cadeia iniciar um loop infinito, o nível de aninhamento será excedido e o gatilho será encerrado.  
  
 Você pode usar gatilhos aninhados para executar funções de manutenção úteis, como armazenar uma cópia de backup de linhas afetadas por um gatilho anterior. Por exemplo, você pode criar um gatilho em `PurchaseOrderDetail` que salva uma cópia de backup das linhas de `PurchaseOrderDetail` que o gatilho `delcascadetrig` excluiu. Com o gatilho `delcascadetrig` em vigor, excluir `PurchaseOrderID` 1965 de `PurchaseOrderHeader` exclui a linha correspondente de `PurchaseOrderDetail`. Para salvar os dados, você pode criar um gatilho DELETE em `PurchaseOrderDetail` que salva os dados excluídos em outra tabela criada separadamente, `del_save`. Por exemplo:  
  
```  
CREATE TRIGGER Purchasing.savedel  
   ON Purchasing.PurchaseOrderDetail  
FOR DELETE  
AS  
   INSERT del_save;  
   SELECT * FROM deleted;  
```  
  
 Nós não recomendamos usar gatilhos aninhados em uma sequência dependente de ordem. Use gatilhos separados para colocar modificações de dados em cascata.  
  
> [!NOTE]  
>  Como os gatilhos são executados em uma transação, uma falha em qualquer nível de um conjunto de gatilhos aninhados cancela toda a transação e todas as modificações de dados são revertidas. Inclua instruções PRINT em seus gatilhos de modo que você possa determinar onde a falha ocorreu.  
  
## <a name="recursive-triggers"></a>Gatilhos recursivos  
 Um gatilho AFTER não pode ser chamado recursivamente a menos que a opção do banco de dados RECURSIVE_TRIGGERS seja definida.  
  
 Existem dois tipos de grupos de recursão:  
  
-   Recursão direta  
  
     Essa recursão ocorre quando um gatilho é acionado e executa uma ação que faz com que o mesmo gatilho seja acionado novamente. Por exemplo, um aplicativo atualiza a tabela **T3**; isso faz com que o gatilho **Trig3** seja acionado. **Trig3** atualiza a tabela **T3** novamente; isso faz com que o gatilho **Trig3** seja acionado novamente.  
  
     A recursão direta também pode ocorrer quando o mesmo gatilho é chamado novamente, mas após um gatilho de um tipo diferente (AFTER ou INSTEAD OF) ter sido chamado. Em outras palavras, a recursão direta de um gatilho INSTEAD OF pode ocorrer quando o mesmo gatilho INSTEAD OF é chamado pela segunda vez, mesmo se um ou mais gatilhos AFTER forem chamados no meio disso. Da mesma maneira, a recursão direta de um gatilho AFTER pode ocorrer quando o mesmo gatilho AFTER é chamado pela segunda vez, mesmo se um ou mais gatilhos INSTEAD OF forem chamados no meio disso. Por exemplo, um aplicativo atualiza a tabela **T4**. Essa atualização faz com que o gatilho INSTEAD OF **Trig4** seja acionado. **Trig4** atualiza a tabela **T5**. Essa atualização faz com que o gatilho AFTER **Trig5** seja acionado. **Trig5** atualiza a tabela **T4**e essa atualização faz com que o gatilho INSTEAD OF **Trig4** seja acionado novamente. Essa cadeia de eventos é considerada uma recursão direta para **Trig4**.  
  
-   Recursão indireta  
  
     Essa recursão ocorre quando um gatilho é acionado e executa uma ação que faz com que outro gatilho do mesmo tipo (AFTER ou INSTEAD OF) seja acionado. Esse segundo gatilho executa uma ação que faz com que o gatilho original seja acionado novamente. Em outras palavras, a recursão indireta pode ocorrer quando um gatilho INSTEAD OF for chamado pela segunda vez, mas não até que outro gatilho INSTEAD OF seja chamado no meio disso. Da mesma maneira, a recursão indireta pode ocorrer quando um gatilho AFTER for chamado pela segunda vez, mas não até que outro gatilho AFTER seja chamado no meio disso. Por exemplo, um aplicativo atualiza a tabela **T1**. Essa atualização faz com que o gatilho AFTER **Trig1** seja acionado. **Trig1** atualiza a tabela **T2**e essa atualização faz com que o gatilho AFTER **Trig2** seja acionado. **Trig2** , por sua vez, atualiza a tabela **T1** , o que faz com que o gatilho AFTER **Trig1** seja acionado novamente.  
  
 Somente a recursão direta de gatilhos AFTER é impedida quando a opção do banco de dados RECURSIVE_TRIGGERS estiver definida como OFF. Para desabilitar a recursão indireta de gatilhos AFTER, defina também a opção do servidor **nested triggers** como **0**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra o uso de gatilhos recursivos para resolver uma relação de autorreferência (também conhecida como fechamento transitivo). Por exemplo, a tabela `emp_mgr` define o seguinte:  
  
-   Um funcionário (`emp`) em uma empresa.  
  
-   O gerente de cada funcionário (`mgr`).  
  
-   O número total de funcionários na árvore organizacional reportando-se a cada funcionário (`NoOfReports`).  
  
 Um gatilho recursivo UPDATE pode ser usado para manter a coluna `NoOfReports` atualizada à medida que novos registros de funcionário forem sendo inseridos. O gatilho INSERT atualiza a coluna `NoOfReports` do registro do gerente, o que atualiza recursivamente a coluna `NoOfReports` de outros registros acima da hierarquia de gerenciamento.  
  
```  
USE AdventureWorks2012;  
GO  
-- Turn recursive triggers ON in the database.  
ALTER DATABASE AdventureWorks2012  
   SET RECURSIVE_TRIGGERS ON;  
GO  
CREATE TABLE dbo.emp_mgr (  
   emp char(30) PRIMARY KEY,  
    mgr char(30) NULL FOREIGN KEY REFERENCES emp_mgr(emp),  
    NoOfReports int DEFAULT 0  
);  
GO  
CREATE TRIGGER dbo.emp_mgrins ON dbo.emp_mgr  
FOR INSERT  
AS  
DECLARE @e char(30), @m char(30);  
DECLARE c1 CURSOR FOR  
   SELECT emp_mgr.emp  
   FROM   emp_mgr, inserted  
   WHERE emp_mgr.emp = inserted.mgr;  
  
OPEN c1;  
FETCH NEXT FROM c1 INTO @e;  
WHILE @@fetch_status = 0  
BEGIN  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports + 1 -- Add 1 for newly  
   WHERE emp_mgr.emp = @e ;                           -- added employee.  
  
   FETCH NEXT FROM c1 INTO @e;  
END  
CLOSE c1;  
DEALLOCATE c1;  
GO  
-- This recursive UPDATE trigger works assuming:  
--   1. Only singleton updates on emp_mgr.  
--   2. No inserts in the middle of the org tree.  
CREATE TRIGGER dbo.emp_mgrupd ON dbo.emp_mgr FOR UPDATE  
AS  
IF UPDATE (mgr)  
BEGIN  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports + 1 -- Increment mgr's  
   FROM inserted                            -- (no. of reports) by  
   WHERE emp_mgr.emp = inserted.mgr;         -- 1 for the new report.  
  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports - 1 -- Decrement mgr's  
   FROM deleted                             -- (no. of reports) by 1  
   WHERE emp_mgr.emp = deleted.mgr;          -- for the new report.  
END  
GO  
-- Insert some test data rows.  
INSERT dbo.emp_mgr(emp, mgr) VALUES  
    ('Harry', NULL)  
    ,('Alice', 'Harry')  
    ,('Paul', 'Alice')  
    ,('Joe', 'Alice')  
    ,('Dave', 'Joe');  
GO  
SELECT emp,mgr,NoOfReports  
FROM dbo.emp_mgr;  
GO  
-- Change Dave's manager from Joe to Harry  
UPDATE dbo.emp_mgr SET mgr = 'Harry'  
WHERE emp = 'Dave';  
GO  
SELECT emp,mgr,NoOfReports FROM emp_mgr;  
  
GO  
```  
  
 Eis os resultados antes da atualização.  
  
```  
emp                            mgr                           NoOfReports  
------------------------------ ----------------------------- -----------  
Alice                          Harry                          2  
Dave                           Joe                            0  
Harry                          NULL                           1  
Joe                            Alice                          1  
Paul                           Alice                          0  
```  
  
 Eis os resultados após a atualização.  
  
```  
emp                            mgr                           NoOfReports  
------------------------------ ----------------------------- -----------  
Alice                          Harry                          2  
Dave                           Harry                          0  
Harry                          NULL                           2  
Joe                            Alice                          0  
Paul                           Alice                          0  
```  
  
 **Para definir a opção de gatilhos aninhados**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
 **Para definir a opção do banco de dados RECURSIVE_TRIGGERS**  
  
-   [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Configurar a opção de configuração de servidor nested triggers](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md)  
  
  
