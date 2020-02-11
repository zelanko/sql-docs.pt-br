---
title: Executando uma instrução | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], executing
ms.assetid: e5f0d2ee-0453-4faf-b007-12978dd300a1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d95226e9d895bf78e15176744f651b7e830a1a10
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901341"
---
# <a name="executing-a-statement"></a>Executar uma instrução
Há quatro maneiras de executar uma instrução, dependendo de quando elas são compiladas (preparadas) pelo mecanismo de banco de dados e quem as define:  
  
-   **Execução direta** O aplicativo define a instrução SQL. Ele é preparado e executado em tempo de execução em uma única etapa.  
  
-   **Execução preparada** O aplicativo define a instrução SQL. Ele é preparado e executado em tempo de execução em etapas separadas. A instrução pode ser preparada uma vez e executada várias vezes.  
  
-   **Procedimentos** do O aplicativo pode definir e compilar uma ou mais instruções SQL em tempo de desenvolvimento e armazenar essas instruções na fonte de dados como um procedimento. O procedimento é executado uma ou mais vezes em tempo de execução. O aplicativo pode enumerar os procedimentos armazenados disponíveis usando funções de catálogo.  
  
-   **Funções de catálogo** O gravador de driver cria uma função que retorna um conjunto de resultados predefinido. Normalmente, essa função envia uma instrução SQL predefinida ou chama um procedimento criado para essa finalidade. A função é executada uma ou mais vezes em tempo de execução.  
  
 Uma determinada instrução (conforme identificado por seu identificador de instrução) pode ser executada várias vezes. A instrução pode ser executada com uma variedade de diferentes instruções SQL ou pode ser executada repetidamente com a mesma instrução SQL. Por exemplo, o código a seguir usa o mesmo identificador de instrução (*hstmt1*) para recuperar e exibir as tabelas no banco de dados Sales. Em seguida, ele reutiliza esse identificador para recuperar as colunas em uma tabela selecionada pelo usuário.  
  
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
  
 E o código a seguir mostra como um único identificador é usado para executar repetidamente a mesma instrução para excluir linhas de uma tabela.  
  
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
  
 Para muitos drivers, as instruções de alocação são uma tarefa cara, portanto, reutilizar a mesma instrução dessa maneira geralmente é mais eficiente do que liberar Instruções existentes e alocar novas. Os aplicativos que criam conjuntos de resultados em uma instrução devem ter cuidado para fechar o cursor sobre o conjunto de resultados antes de executar novamente a instrução; para obter mais informações, consulte [fechando o cursor](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 Reutilizar instruções também força o aplicativo a evitar uma limitação em alguns drivers do número de instruções que podem estar ativas ao mesmo tempo. A definição exata de "active" é específica do driver, mas geralmente se refere a qualquer instrução que tenha sido preparada ou executada e que ainda tenha resultados disponíveis. Por exemplo, após uma instrução **Insert** ter sido preparada, ela é geralmente considerada ativa; Depois que uma instrução **Select** tiver sido executada e o cursor ainda estiver aberto, geralmente será considerado como ativo; após a execução de uma instrução **CREATE TABLE** , ela não é geralmente considerada ativa.  
  
 Um aplicativo determina quantas instruções podem estar ativas em uma única conexão ao mesmo tempo chamando **SQLGetInfo** com a opção SQL_MAX_CONCURRENT_ACTIVITIES. Um aplicativo pode usar mais instruções ativas do que esse limite abrindo várias conexões com a fonte de dados; no entanto, como as conexões podem ser caras, o efeito no desempenho deve ser considerado.  
  
 Os aplicativos podem limitar a quantidade de tempo alocada para que uma instrução seja executada com o atributo de instrução SQL_ATTR_QUERY_TIMEOUT. Se o período de tempo limite expirar antes que a fonte de dados retorne o conjunto de resultados, a função que executa a instrução SQL retornará SQLSTATE HYT00 (timeout expirado). Por padrão, não há nenhum tempo limite.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Execução direta](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [Execução preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [Procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [Lotes de instruções SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [Executar funções de catálogo](../../../odbc/reference/develop-app/executing-catalog-functions.md)
