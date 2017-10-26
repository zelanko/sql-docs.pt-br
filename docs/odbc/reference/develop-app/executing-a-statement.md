---
title: "Executar uma instrução | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], executing
ms.assetid: e5f0d2ee-0453-4faf-b007-12978dd300a1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8e3fdaf1a063951dcb06018858a905c5ee8651e9
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="executing-a-statement"></a>Executar uma instrução
Há quatro maneiras de executar uma instrução, dependendo de quando são compiladas (preparada), o mecanismo de banco de dados e que defini-los:  
  
-   **Direcionar a execução** o aplicativo define a instrução SQL. Ele é preparado e executado em tempo de execução em uma única etapa.  
  
-   **A execução preparada** o aplicativo define a instrução SQL. Ele é preparado e executado em tempo de execução em etapas separadas. A instrução pode ser preparada uma vez e executada várias vezes.  
  
-   **Procedimentos** o aplicativo pode definir e compilar uma ou mais instruções SQL no desenvolvimento de tempo e armazenam essas instruções na fonte de dados como um procedimento. O procedimento é executado uma ou mais vezes em tempo de execução. O aplicativo pode enumerar os procedimentos armazenados disponíveis usando funções de catálogo.  
  
-   **Funções de catálogo** o gravador de driver cria uma função que retorna um conjunto de resultados predefinidos. Normalmente, essa função envia uma instrução SQL predefinida ou chama um procedimento criado para essa finalidade. A função é executada uma ou mais vezes em tempo de execução.  
  
 Uma instrução específica (conforme identificado pelo seu identificador de instrução) pode ser executado várias vezes. A instrução pode ser executada com uma variedade de instruções SQL diferentes, ou pode ser executado repetidamente com a mesma instrução SQL. Por exemplo, o código a seguir usa o mesmo identificador de instrução (*hstmt1*) para recuperar e exibir as tabelas no banco de dados de vendas. Em seguida, ele reutiliza esse identificador para recuperar as colunas em uma tabela selecionada pelo usuário.  
  
```  
SQLHSTMT    hstmt1;  
SQLCHAR *   Table;  
  
// Create a result set of all tables in the Sales database.  
SQLTables(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, NULL, 0, NULL, 0);  
  
// Fetch and display the table names; then close the cursor.  
// Code not shown.  
  
// Have the user select a particular table.  
SelectTable(Table);  
  
// Reuse hstmt1 to create a result set of all columns in Table.  
SQLColumns(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, Table, SQL_NTS, NULL, 0);  
  
// Fetch and display the column names in Table; then close the cursor.  
// Code not shown.  
```  
  
 E o código a seguir mostra como um identificador único é usado para executar repetidamente a mesma instrução para excluir linhas de uma tabela.  
  
```  
SQLHSTMT      hstmt1;  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
  
// Prepare a statement to delete orders from the Orders table.  
SQLPrepare(hstmt1, "DELETE FROM Orders WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter for the OrderID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &OrderID, 0, &OrderIDInd);  
  
// Repeatedly execute hstmt1 with different values of OrderID.  
while ((OrderID = GetOrderID()) != 0) {  
   SQLExecute(hstmt1);  
}  
```  
  
 Para muitos drivers, alocar instruções é uma tarefa cara, para que reutilizar a mesma instrução dessa maneira é geralmente mais eficiente do que liberando instruções existentes e novos de alocação. Aplicativos que criam conjuntos de resultados em uma instrução devem ter cuidadosos ao fechar o cursor sobre o conjunto de resultados antes de executar novamente a instrução; Para obter mais informações, consulte [fechar o Cursor](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 Reutilizar instruções também força o aplicativo para evitar uma limitação no alguns drivers do número de instruções que podem estar ativas simultaneamente. A definição exata de "ativo" é específico do driver, mas geralmente se refere a qualquer instrução preparada ou executada e ainda tem resultados disponíveis. Por exemplo, após um **inserir** instrução foi preparada, ele geralmente é considerado como ativo; depois um **selecione** instrução foi executada e o cursor ainda estiver aberto, ela é geralmente considerada estar ativo; Depois que um **CREATE TABLE** instrução foi executada, ele geralmente não é considerado como ativo.  
  
 Um aplicativo determina quantas instruções podem estar ativas em uma única conexão de uma só vez chamando **SQLGetInfo** com a opção SQL_MAX_CONCURRENT_ACTIVITIES. Um aplicativo pode usar instruções mais ativas que esse limite abrindo várias conexões com a fonte de dados; como conexões podem ser caros, no entanto, o efeito de desempenho deve ser considerado.  
  
 Aplicativos podem limitar a quantidade de tempo alocado para uma instrução executar com o atributo de instrução SQL_ATTR_QUERY_TIMEOUT. Se o período de tempo limite expirar antes que a fonte de dados retorna o conjunto de resultados, a função executa a instrução SQL retornará SQLSTATE HYT00 (tempo limite expirado). Por padrão, não há nenhum tempo limite.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Execução direta](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [Execução preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [Procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [Lotes de instruções SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [Executando funções de catálogo](../../../odbc/reference/develop-app/executing-catalog-functions.md)

