---
title: Executando uma Declaração | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3ce09809c896a4d1d9333da00367f972655f96b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305737"
---
# <a name="executing-a-statement"></a>Executar uma instrução
Existem quatro maneiras de executar uma declaração, dependendo de quando elas são compiladas (preparadas) pelo mecanismo do banco de dados e quem as define:  
  
-   **Execução Direta** O aplicativo define a declaração SQL. É preparado e executado em tempo de execução em uma única etapa.  
  
-   **Execução Preparada** O aplicativo define a declaração SQL. É preparado e executado em tempo de execução em etapas separadas. A declaração pode ser preparada uma vez e executada várias vezes.  
  
-   **Procedimentos** O aplicativo pode definir e compilar uma ou mais instruções SQL no momento do desenvolvimento e armazenar essas instruções na fonte de dados como um procedimento. O procedimento é executado uma ou mais vezes no tempo de execução. O aplicativo pode enumerar procedimentos armazenados disponíveis usando funções de catálogo.  
  
-   **Funções do catálogo** O driver writer cria uma função que retorna um conjunto de resultados predefinido. Normalmente, essa função envia uma declaração SQL predefinida ou chama um procedimento criado para esse fim. A função é executada uma ou mais vezes no tempo de execução.  
  
 Uma declaração específica (identificada pelo seu identificador de declaração) pode ser executada várias vezes. A instrução pode ser executada com uma variedade de diferentes instruções SQL, ou pode ser executada repetidamente com a mesma instrução SQL. Por exemplo, o código a seguir usa a mesma alça de declaração *(hstmt1)* para recuperar e exibir as tabelas no banco de dados de Vendas. Em seguida, ele reutiliza esta alça para recuperar as colunas em uma tabela selecionada pelo usuário.  
  
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
  
 E o código a seguir mostra como uma única alça é usada para executar repetidamente a mesma declaração para excluir linhas de uma tabela.  
  
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
  
 Para muitos drivers, alocar declarações é uma tarefa cara, então reutilizar a mesma declaração dessa maneira geralmente é mais eficiente do que liberar declarações existentes e alocar novas. Os aplicativos que criam conjuntos de resultados em uma declaração devem ter o cuidado de fechar o cursor sobre o conjunto de resultados antes de reexecutar a declaração; para obter mais informações, consulte [Fechando o Cursor](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 A reutilização de declarações também força o aplicativo a evitar uma limitação em alguns drivers do número de declarações que podem estar ativas ao mesmo tempo. A definição exata de "ativo" é específica do driver, mas muitas vezes se refere a qualquer declaração que tenha sido preparada ou executada e ainda tenha resultados disponíveis. Por exemplo, depois que uma instrução **INSERT** foi preparada, ela é geralmente considerada ativa; depois que uma declaração **SELECT** foi executada e o cursor ainda está aberto, ele é geralmente considerado ativo; depois que uma declaração **DE TABELA CREATE** foi executada, ela não é geralmente considerada ativa.  
  
 Um aplicativo determina quantas instruções podem estar ativas em uma única conexão de uma só vez, ligando para **o SQLGetInfo** com a opção SQL_MAX_CONCURRENT_ACTIVITIES. Um aplicativo pode usar mais instruções ativas do que esse limite, abrindo várias conexões à fonte de dados; porque as conexões podem ser caras, no entanto, o efeito sobre o desempenho deve ser considerado.  
  
 Os aplicativos podem limitar a quantidade de tempo atribuída para uma declaração ser executada com o atributo de declaração SQL_ATTR_QUERY_TIMEOUT. Se o período de tempo expirar antes que a fonte de dados retorne o conjunto de resultados, a função que executa a declaração SQL retorna SQLSTATE HYT00 (O tempo expirado). Por padrão, não há nenhum tempo limite.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Execução direta](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [Execução preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [Procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [Lotes de instruções SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [Executar funções de catálogo](../../../odbc/reference/develop-app/executing-catalog-functions.md)
