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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09805ab73af76bc55890222fc1ffd0e1857d0f33
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62447384"
---
# <a name="batches-of-sql-statements"></a>Lotes de instruções SQL
Um lote de instruções SQL é um grupo de duas ou mais instruções SQL ou uma única instrução SQL que tem o mesmo efeito de um grupo de duas ou mais instruções SQL. Em algumas implementações, a instrução do lote inteiro é executada antes que todos os resultados estejam disponíveis. Isso geralmente é mais eficiente do que enviar instruções separadamente, pois o tráfego de rede geralmente pode ser reduzido e a fonte de dados, às vezes, pode otimizar a execução de um lote de instruções SQL. Em outras implementações, chamando **SQLMoreResults** dispara a execução da próxima instrução no lote. ODBC dá suporte aos seguintes tipos de lotes:  
  
-   **Lotes explícitos** uma *lote explícito* é dois ou mais instruções SQL separadas por ponto e vírgula (;). Por exemplo, o lote de instruções SQL a seguir abre uma nova ordem de venda. Isso requer inserindo linhas em tabelas de pedidos e linhas. Observe que não há nenhum ponto e vírgula após a última instrução.  
  
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
  
-   **Procedimentos** se um procedimento contiver mais de uma instrução SQL, ele é considerado um lote de instruções SQL. Por exemplo, a instrução específica do SQL Server a seguir cria um procedimento que retorna um conjunto de resultados contendo informações sobre um cliente e um resultado definido listando todos os pedidos de vendas abertos desse cliente:  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     O **CREATE PROCEDURE** instrução em si não é um lote de instruções SQL. No entanto, o procedimento que ele cria é um lote de instruções SQL. Nenhum ponto e vírgula separar as duas **selecionar** instruções porque o **CREATE PROCEDURE** instrução é específica para o SQL Server e do SQL Server não requer um ponto e vírgula para separar várias instruções em um  **CREATE PROCEDURE** instrução.  
  
-   **Matrizes de parâmetros** matrizes de parâmetros podem ser usados com uma instrução SQL parametrizada como uma maneira eficiente para executar operações em massa. Por exemplo, as matrizes de parâmetros podem ser usados com o seguinte **inserir** instrução inserir várias linhas na tabela de linhas durante a execução de uma única instrução SQL:  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     Se uma fonte de dados não der suporte a matrizes de parâmetros, o driver poderá emulá-los executando a instrução SQL, uma vez para cada conjunto de parâmetros. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md) e [matrizes de valores de parâmetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md), mais adiante nesta seção.  
  
 Os diferentes tipos de lotes não podem ser combinados de maneira interoperável. Ou seja, como um aplicativo determina o resultado da execução de um lote explícito que inclui um procedimento chama, um lote explícito que usa matrizes de parâmetros, e uma chamada de procedimento que usa matrizes de parâmetros é específica do driver.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Instruções de geração de resultado e sem resultados](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [Lotes em execução](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [Erros e lotes](../../../odbc/reference/develop-app/errors-and-batches.md)
