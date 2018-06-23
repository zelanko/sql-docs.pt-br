---
title: Criar gatilhos DML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-dml
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 30
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 9fdbff3f7bc6957a72c4bfb674552f6a213e41d6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116339"
---
# <a name="create-dml-triggers"></a>Criar gatilhos DML
  Este tópico descreve como criar um gatilho DML [!INCLUDE[tsql](../../includes/tsql-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TRIGGER.  
  
##  <a name="Top"></a> Antes de começar  
  
### <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Para obter uma lista de limitações e restrições relacionadas à criação de gatilhos DML, veja [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql).  
  
###  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela ou exibição na qual o gatilho é criado.  
  
##  <a name="Procedures"></a> Como criar um gatilho DML  
 Você pode usar uma das seguintes opções:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, expanda o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , expanda **Tabelas** e expanda a tabela **Purchasing.PurchaseOrderHeader**.  
  
3.  Clique com o botão direito do mouse em **Gatilhos**e selecione **Novo Gatilho**.  
  
4.  No menu **Consulta** , clique em **Especificar Valores para Parâmetros de Modelo**. Como alternativa, pressione (Ctrl-Shift-M) para abrir caixa de diálogo **Especificar Valores para Parâmetros de Modelo** .  
  
5.  Na caixa de diálogo **Especificar Valores para Parâmetros de Modelo** , digite os seguintes valores para os parâmetros mostrados.  
  
    |Parâmetro|Valor|  
    |---------------|-----------|  
    |Autor|*Seu nome*|  
    |Data de criação|*A data de hoje*|  
    |Description|Verifica a avaliação de crédito de fornecedor antes de permitir uma nova ordem de compra com o fornecedor a ser inserido.|  
    |Schema_Name|Purchasing|  
    |Trigger_Name|NewPODetail2|  
    |Table_Name|PurchaseOrderDetail|  
    |Data_Modification_Statement|Remova UPDATE e DELETE da lista.|  
  
6.  Clique em **OK**.  
  
7.  No **Editor de Consultas**, substitua o comentário `-- Insert statements for trigger here` pela seguinte instrução:  
  
    ```tsql  
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
  
###  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] e expanda-a.  
  
2.  No menu **Arquivo** , clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo cria o mesmo gatilho DML armazenado como anteriormente.  
  
    ```  
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
  
##  <a name="PowerShellProcedure"></a> [Antes de começar](#Top)  
  
  
