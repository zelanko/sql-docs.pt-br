---
title: "Criar gatilhos DML para tratar várias linhas de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiple row DML triggers
- UPDATE statement [SQL Server], DML triggers
- DELETE statement [SQL Server], DML triggers
- multirow DML triggers [SQL Server]
- INSERT statement [SQL Server], DML triggers
- DML triggers, multirow
ms.assetid: d476c124-596b-4b27-a883-812b6b50a735
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8f8f36c8882e981ba4096fdccab4bed5801ebc9e
ms.lasthandoff: 04/11/2017

---
# <a name="create-dml-triggers-to-handle-multiple-rows-of-data"></a>Crie gatilhos DML para tratar várias linhas de dados
  Ao gravar o código de um gatilho DML, considere que a instrução que aciona o gatilho pode ser uma única instrução que afeta diversas linhas de dados, em vez de uma única linha. Esse comportamento é comum para os gatilhos UPDATE e DELETE, pois essas instruções geralmente afetam várias linhas. O comportamento é menos comum para gatilhos INSERT, pois a instrução INSERT básica adiciona apenas uma única linha. Entretanto, como o gatilho INSERT pode ser acionado por uma instrução INSERT INTO (*table_name*) SELECT, a inserção de várias linhas pode causar a invocação de um único gatilho.  
  
 Considerações multilinha são especialmente importantes quando a função de um gatilho DML deve ser recalcular automaticamente valores de resumo de uma tabela e armazenar os resultados em outra para contagens contínuas.  
  
> [!NOTE]  
>  Não recomendamos usar cursores em gatilhos porque eles potencialmente podem reduzir o desempenho. Para projetar um gatilho que afeta várias linhas, use uma lógica baseada em conjunto de linhas em vez de cursores.  
  
## <a name="examples"></a>Exemplos  
 Os gatilhos DML nos exemplos a seguir são projetados para armazenar o total de execução de uma coluna em outra tabela do banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
### <a name="a-storing-a-running-total-for-a-single-row-insert"></a>A. Armazenando um total de execução de uma inserção de única linha  
 A primeira versão do gatilho DML trabalha bem para uma inserção de única linha quando uma linha de dados é carregada na tabela `PurchaseOrderDetail` . Uma instrução INSERT aciona um gatilho DML e uma nova linha é carregada na tabela **inserida** durante o período de duração da execução do gatilho. A instrução `UPDATE` lê o valor da coluna `LineTotal` para a linha e adiciona esse valor ao valor existente na coluna `SubTotal` na tabela `PurchaseOrderHeader` . A cláusula `WHERE` certifica que a linha atualizada na tabela `PurchaseOrderDetail` corresponde à `PurchaseOrderID` da linha na tabela **inserida** .  
  
```  
-- Trigger is valid for single-row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail  
ON Purchasing.PurchaseOrderDetail  
AFTER INSERT AS  
   UPDATE PurchaseOrderHeader  
   SET SubTotal = SubTotal + LineTotal  
   FROM inserted  
   WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID ;  
```  
  
### <a name="b-storing-a-running-total-for-a-multirow-or-single-row-insert"></a>B. Armazenando um total de execução para uma inserção multilinha ou de linha única  
 Para uma inserção de várias linhas, o gatilho DML no exemplo A pode não funcionar corretamente; a expressão à direita de uma expressão de atribuição em uma instrução UPDATE (`SubTotal` + `LineTotal`) pode ser apenas um único valor, não uma lista de valores. Portanto, o efeito do gatilho é para recuperar um valor de qualquer linha única na tabela **inserida** e adicionar esse valor a um valor de `SubTotal` existente na tabela `PurchaseOrderHeader` para um valor específico `PurchaseOrderID` . Essa operação pode não ter o efeito esperado se um único valor de `PurchaseOrderID` ocorrer mais de uma vez na tabela **inserida** .  
  
 Para atualizar corretamente a tabela `PurchaseOrderHeader` , o gatilho deve permitir várias linhas na tabela **inserida** . Você pode fazer isso usando a função `SUM` que calcula o total de um grupo de linhas `LineTotal` na tabela **inserida** de cada `PurchaseOrderID`. A função `SUM` é incluída em uma subconsulta correlacionada (a instrução `SELECT` entre parênteses). Esta subconsulta retorna um único valor para cada `PurchaseOrderID` na tabela **inserida** que corresponde ou está correlacionada a `PurchaseOrderID` na tabela `PurchaseOrderHeader` .  
  
```  
-- Trigger is valid for multirow and single-row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail2  
ON Purchasing.PurchaseOrderDetail  
AFTER INSERT AS  
   UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal +   
      (SELECT SUM(LineTotal)  
      FROM inserted  
      WHERE PurchaseOrderHeader.PurchaseOrderID  
       = inserted.PurchaseOrderID)  
   WHERE PurchaseOrderHeader.PurchaseOrderID IN  
      (SELECT PurchaseOrderID FROM inserted);  
```  
  
 Esse gatilho também funciona corretamente em uma inserção de única linha; a soma da coluna de valor `LineTotal` é a soma de uma única linha. Entretanto, com esse gatilho a subconsulta correlacionada e o operador `IN` usado na cláusula `WHERE` exigem processamento adicional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isto é desnecessário para uma inserção da única-linha.  
  
### <a name="c-storing-a-running-total-based-on-the-type-of-insert"></a>C. Armazenando um total de execução com base no tipo de inserção  
 Você pode alterar o gatilho para usar o método ideal para o número de linhas. Por exemplo, a função `@@ROWCOUNT` pode ser usada na lógica do gatilho para distinguir entre uma inserção única e multilinha.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Gatilhos DML](../../relational-databases/triggers/dml-triggers.md)  
  
  
