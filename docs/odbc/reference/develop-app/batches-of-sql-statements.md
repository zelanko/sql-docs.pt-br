---
title: Lotes de Declarações SQL | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283506"
---
# <a name="batches-of-sql-statements"></a>Lotes de instruções SQL
Um lote de instruções SQL é um grupo de duas ou mais instruções SQL ou uma única instrução SQL que tem o mesmo efeito que um grupo de duas ou mais instruções SQL. Em algumas implementações, toda a declaração do lote é executada antes de qualquer resultado disponível. Isso é muitas vezes mais eficiente do que enviar declarações separadamente, porque o tráfego de rede muitas vezes pode ser reduzido e a fonte de dados às vezes pode otimizar a execução de um lote de instruções SQL. Em outras implementações, chamar **SQLMoreResults** desencadeia a execução da próxima declaração no lote. O ODBC suporta os seguintes tipos de lotes:  
  
-   **Lotes explícitos** Um *lote explícito* são duas ou mais instruções SQL separadas por ponto e vírgula (;). Por exemplo, o lote a seguir de demonstrações SQL abre uma nova ordem de venda. Isso requer a inserção de linhas nas tabelas Ordens e Linhas. Note que não há ponto e vírgula após a última declaração.  
  
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
  
-   **Procedimentos** Se um procedimento contiver mais de uma instrução SQL, é considerado um lote de instruções SQL. Por exemplo, a seguinte instrução específica do SQL Server cria um procedimento que retorna um conjunto de resultados contendo informações sobre um cliente e um conjunto de resultados listando todas as ordens de venda abertas para esse cliente:  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     A instrução **CREATE PROCEDURE** em si não é um lote de instruções SQL. No entanto, o procedimento que ele cria é um lote de instruções SQL. Nenhum ponto e vírgula separa as duas instruções **SELECT** porque a instrução **CREATE PROCEDURE** é específica para o SQL Server, e o SQL Server não requer ponto e vírgula para separar várias instruções em uma instrução **CREATE PROCEDURE.**  
  
-   **Matrizes de parâmetros** Conjuntos de parâmetros podem ser usados com uma declaração SQL parametrizada como uma maneira eficaz de realizar operações em massa. Por exemplo, conjuntos de parâmetros podem ser usados com a seguinte instrução **INSERT** para inserir várias linhas na tabela Linhas enquanto executa apenas uma única instrução SQL:  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     Se uma fonte de dados não suportar matrizes de parâmetros, o driver pode emulá-los executando a declaração SQL uma vez para cada conjunto de parâmetros. Para obter mais informações, consulte [Parâmetros](../../../odbc/reference/develop-app/statement-parameters.md) de declaração e [matrizes de valores de parâmetros,](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)mais tarde nesta seção.  
  
 Os diferentes tipos de lotes não podem ser misturados de forma interoperável. Ou seja, como um aplicativo determina o resultado da execução de um lote explícito que inclui chamadas de procedimento, um lote explícito que usa matrizes de parâmetros e uma chamada de procedimento que usa matrizes de parâmetros é específica do driver.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Instruções de geração de resultado e sem resultados](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [Lotes em execução](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [Erros e lotes](../../../odbc/reference/develop-app/errors-and-batches.md)
