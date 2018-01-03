---
title: "Lotes de instruções SQL | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- batches [ODBC]
- SQL statements [ODBC], batches
- batches [ODBC], about batches
ms.assetid: 766488cc-450c-434c-9c88-467f6c57e17c
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d2ae8d60d6e41536bc67bd14f9252c372fdeaa5c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="batches-of-sql-statements"></a>Lotes de instruções SQL
Um lote de instruções SQL é um grupo de duas ou mais instruções SQL ou uma única instrução SQL que tem o mesmo efeito de um grupo de duas ou mais instruções SQL. Em algumas implementações, a instrução de lote inteiro é executada antes de todos os resultados estão disponíveis. Isso geralmente é mais eficiente que enviar instruções separadamente, pois o tráfego de rede geralmente pode ser reduzido e a fonte de dados, às vezes, pode otimizar a execução de um lote de instruções SQL. Em outras implementações, chamando **SQLMoreResults** dispara a execução da próxima instrução no lote. ODBC suporta os seguintes tipos de lotes:  
  
-   **Lotes explícitas** um *lote explícito* é duas ou mais instruções SQL separadas por ponto e vírgula (;). Por exemplo, o lote de instruções SQL a seguir abre um novo pedido de vendas. Isso requer inserir linhas em tabelas de pedidos e de linhas. Observe que não há nenhum ponto e vírgula após a última instrução.  
  
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
  
-   **Procedimentos** se um procedimento contiver mais de uma instrução SQL, ele é considerado um lote de instruções SQL. Por exemplo, a instrução a seguir específicas do SQL Server cria um procedimento que retorna um conjunto de resultados contendo informações sobre um cliente e um conjunto listando todos os pedidos de vendas abertos para esse cliente de resultados:  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     O **CREATE PROCEDURE** instrução em si não é um lote de instruções SQL. No entanto, o procedimento cria é um lote de instruções SQL. Nenhum ponto e vírgula separe os dois **selecione** instruções porque o **CREATE PROCEDURE** instrução é específica ao SQL Server e do SQL Server não requer um ponto e vírgula para separar várias instruções em um  **CREATE PROCEDURE** instrução.  
  
-   **Matrizes de parâmetros** matrizes de parâmetros podem ser usados com uma instrução SQL parametrizada como uma maneira eficiente para executar operações em massa. Por exemplo, as matrizes de parâmetros podem ser usados com os seguintes **inserir** instrução inserir várias linhas na tabela de linhas durante a execução de uma única instrução SQL:  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     Se uma fonte de dados não oferece suporte a matrizes de parâmetros, o driver pode emulá-los, executando a instrução SQL, uma vez para cada conjunto de parâmetros. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md) e [matrizes de valores de parâmetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md), mais adiante nesta seção.  
  
 Os diferentes tipos de lotes não podem ser misturados de maneira interoperável. Ou seja, como um aplicativo determina o resultado da execução de um lote explícito que inclui um procedimento chama, um lote explícito que usa matrizes de parâmetros, e uma chamada de procedimento que usa matrizes de parâmetros é específico do driver.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Instruções de geração de resultado e sem resultados](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [Lotes em execução](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [Erros e lotes](../../../odbc/reference/develop-app/errors-and-batches.md)
