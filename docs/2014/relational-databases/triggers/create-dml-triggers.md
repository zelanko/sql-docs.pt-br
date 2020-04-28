---
title: Criar gatilhos DML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], DML triggers
- deferred name resolution, DML triggers
- WITH ENCRYPTION clause
- IF UPDATE
- SET statement, DML triggers
- DML triggers, programming
- testing column changes
- results [SQL Server], DML triggers
ms.assetid: b2b52258-642b-462e-8e0f-18c09d2eccf4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 10399a26335912a9370aa21a386f58d04d04321e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72796393"
---
# <a name="create-dml-triggers"></a>Criar gatilhos DML
  Este tópico descreve como criar um gatilho DML [!INCLUDE[tsql](../../includes/tsql-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TRIGGER.  
  
##  <a name="before-you-begin"></a><a name="Top"></a> Antes de começar  
  
### <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 Para obter uma lista de limitações e restrições relacionadas à criação de gatilhos DML, veja [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql).  
  
###  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela ou exibição na qual o gatilho é criado.  
  
##  <a name="how-to-create-a-dml-trigger"></a><a name="Procedures"></a> Como criar um gatilho DML  
 Você pode usar uma das seguintes opções:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, expanda o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , expanda **Tabelas** e expanda a tabela **Purchasing.PurchaseOrderHeader**.  
  
3.  Clique com o botão direito do mouse em **Gatilhos**e selecione **Novo Gatilho**.  
  
4.  No menu **Consulta** , clique em **Especificar Valores para Parâmetros de Modelo**. Como alternativa, pressione (Ctrl-Shift-M) para abrir caixa de diálogo **Especificar Valores para Parâmetros de Modelo** .  
  
5.  Na caixa de diálogo **Especificar Valores para Parâmetros de Modelo** , digite os seguintes valores para os parâmetros mostrados.  
  
    |Parâmetro|Valor|  
    |---------------|-----------|  
    |Autor|*Seu nome*|  
    |Data de criação|*A data de hoje*|  
    |DESCRIÇÃO|Verifica a avaliação de crédito de fornecedor antes de permitir uma nova ordem de compra com o fornecedor a ser inserido.|  
    |Schema_Name|Compra|  
    |Trigger_Name|NewPODetail2|  
    |Table_Name|PurchaseOrderDetail|  
    |Data_Modification_Statement|Remova UPDATE e DELETE da lista.|  
  
6.  Clique em **OK**.  
  
7.  No **Editor de Consultas**, substitua o comentário `-- Insert statements for trigger here` pela seguinte instrução:  
  
    ```sql  
    IF @@ROWCOUNT = 1  
    BEGIN  
       UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal + LineTotal  
       FROM inserted  
       WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
  
    END  
    ELSE  
    BEGIN  
          UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal +   
          (SELECT SUM(LineTotal)  
          FROM inserted  
          WHERE PurchaseOrderHeader.PurchaseOrderID  
           = inserted.PurchaseOrderID)  
       WHERE PurchaseOrderHeader.PurchaseOrderID IN  
          (SELECT PurchaseOrderID FROM inserted)  
    END;  
    ```  
  
8.  Para verificar se a sintaxe é válida, no menu **Consulta** , clique em **Analisar**. Se uma mensagem de erro for retornada, compare a instrução com as informações acima e corrija conforme necessário. Repita esta etapa.  
  
9. Para criar o gatilho DML, no menu **Consulta** , clique em **Executar**. O gatilho DML é criado como um objeto no banco de dados.  
  
10. Para ver o gatilho DML listado no Pesquisador de Objetos, clique com o botão direito do mouse em **Gatilhos** e selecione **Atualizar**.  
  
 [Antes de começar](#Top)  
  
###  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] e expanda-a.  
  
2.  No menu **Arquivo** , clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo cria o mesmo gatilho DML armazenado como anteriormente.  
  
    ```sql
    -- Trigger valid for multirow and single row inserts  
    -- and optimal for single row inserts.  
    USE AdventureWorks2012;  
    GO  
    CREATE TRIGGER NewPODetail3  
    ON Purchasing.PurchaseOrderDetail  
    FOR INSERT AS  
    IF @@ROWCOUNT = 1  
    BEGIN  
       UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal + LineTotal  
       FROM inserted  
       WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
  
    END  
    ELSE  
    BEGIN  
          UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal +   
          (SELECT SUM(LineTotal)  
          FROM inserted  
          WHERE PurchaseOrderHeader.PurchaseOrderID  
           = inserted.PurchaseOrderID)  
       WHERE PurchaseOrderHeader.PurchaseOrderID IN  
          (SELECT PurchaseOrderID FROM inserted)  
    END;  
    ```  
