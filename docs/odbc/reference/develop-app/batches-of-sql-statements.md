---
title: Lotes de instruções SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC]
- SQL statements [ODBC], batches
- batches [ODBC], about batches
ms.assetid: 766488cc-450c-434c-9c88-467f6c57e17c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d68ea1c13655ca7c57ba076823f461a4b2e22055
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283506"
---
# <a name="batches-of-sql-statements"></a>Lotes de instruções SQL
Um lote de instruções SQL é um grupo de duas ou mais instruções SQL ou uma única instrução SQL que tem o mesmo efeito que um grupo de duas ou mais instruções SQL. Em algumas implementações, toda a instrução batch é executada antes de qualquer resultado estar disponível. Isso geralmente é mais eficiente do que o envio de instruções separadamente, pois o tráfego de rede geralmente pode ser reduzido e a fonte de dados pode, às vezes, otimizar a execução de um lote de instruções SQL. Em outras implementações, chamar **SQLMoreResults** aciona a execução da próxima instrução no lote. O ODBC dá suporte aos seguintes tipos de lotes:  
  
-   **Lotes explícitos** Um *lote explícito* é duas ou mais instruções SQL separadas por ponto e vírgula (;). Por exemplo, o seguinte lote de instruções SQL abre uma nova ordem de venda. Isso exige a inserção de linhas nas tabelas Orders e Lines. Observe que não há ponto-e-vírgula após a última instrução.  
  
    ```  
    INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
       VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 1, 1234, 10);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 2, 987, 8);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 3, 566, 17);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 4, 412, 500)  
    ```  
  
-   **Procedimentos** do Se um procedimento contiver mais de uma instrução SQL, será considerado um lote de instruções SQL. Por exemplo, a instrução específica a seguir SQL Server cria um procedimento que retorna um conjunto de resultados que contém informações sobre um cliente e um conjunto de resultados listando todos os pedidos de vendas em aberto para esse cliente:  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     A instrução **CREATE PROCEDURE** em si não é um lote de instruções SQL. No entanto, o procedimento que ele cria é um lote de instruções SQL. Nenhum ponto-e-vírgula separa as duas instruções **Select** porque a instrução **CREATE PROCEDURE** é específica para SQL Server e SQL Server não requer ponto e vírgula para separar várias instruções em uma instrução **CREATE PROCEDURE** .  
  
-   **Matrizes de parâmetros** Matrizes de parâmetros podem ser usadas com uma instrução SQL parametrizada como uma maneira eficaz de executar operações em massa. Por exemplo, matrizes de parâmetros podem ser usadas com a seguinte instrução **Insert** para inserir várias linhas na tabela de linhas durante a execução de uma única instrução SQL:  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     Se uma fonte de dados não oferecer suporte a matrizes de parâmetros, o driver poderá emular-os executando a instrução SQL uma vez para cada conjunto de parâmetros. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md) e [matrizes de valores de parâmetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md), mais adiante nesta seção.  
  
 Os diferentes tipos de lotes não podem ser misturados de maneira interoperável. Ou seja, como um aplicativo determina o resultado da execução de um lote explícito que inclui chamadas de procedimento, um lote explícito que usa matrizes de parâmetros e uma chamada de procedimento que usa matrizes de parâmetros é específica do driver.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Instruções de geração de resultado e sem resultados](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [Lotes em execução](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [Erros e lotes](../../../odbc/reference/develop-app/errors-and-batches.md)
