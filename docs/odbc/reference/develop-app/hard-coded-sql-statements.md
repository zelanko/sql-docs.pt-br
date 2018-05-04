---
title: Instruções SQL Hard-Coded | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], hard-coded
- hard-coded SQL statements [ODBC]
- SQL statements [ODBC], constructing
ms.assetid: e355f5f1-4f1a-4933-8c74-ee73e90d2d19
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7b3983a96c1d1337ead09477e10bb65b7033d37
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="hard-coded-sql-statements"></a>Instruções SQL embutidas
Aplicativos que executam uma tarefa fixa geralmente contêm instruções de SQL embutido. Por exemplo, um sistema de entrada de pedidos pode usar a seguinte chamada a pedidos de vendas Abrir lista:  
  
```  
SQLExecDirect(hstmt, "SELECT OrderID FROM Orders WHERE Status = 'OPEN'", SQL_NTS);  
```  
  
 Há várias vantagens para instruções de SQL embutido: eles podem ser testados quando o aplicativo é escrito; eles são mais simples de implementar do que instruções construídas em tempo de execução; e eles simplificam o aplicativo.  
  
 Usando parâmetros de instrução e preparando instruções fornecem ainda mais maneiras de usar instruções de SQL embutido. Por exemplo, suponha que a tabela de peças contém as colunas PartID, descrição e preço. Uma maneira de inserir uma nova linha nessa tabela seria construir e executar um **inserir** instrução:  
  
```  
#define DESC_LEN 51  
#define STATEMENT_LEN 51  
  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN], Statement[STATEMENT_LEN];  
SQLREAL       Price;  
  
// Set part ID, description, and price.  
GetNewValues(&PartID, Desc, &Price);  
  
// Build INSERT statement.  
sprintf_s(Statement, 100, "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (%d, '%s', %f)", PartID, Desc, Price);  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
```  
  
 Uma maneira ainda melhor é usar uma instrução parametrizada embutida. Isso tem duas vantagens sobre uma instrução com valores de dados embutidos. Primeiro, é mais fácil construir uma instrução parametrizada porque os valores de dados podem ser enviados em seus tipos nativos, como números inteiros e números de ponto flutuante, em vez de convertê-las em cadeias de caracteres. Em segundo lugar, tal uma instrução pode ser usada mais de uma vez simplesmente, alterando os valores de parâmetro e executar novamente. Não há nenhuma necessidade de recriá-lo.  
  
```  
#define DESC_LEN 51  
  
SQLCHAR * Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (?, ?, ?)";  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Set part ID, description, and price.  
GetNewValues(&PartID, Desc, &Price);  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
```  
  
 Supondo que essa instrução será executada mais de uma vez, ele pode estar preparado para ainda maior eficiência:  
  
```  
#define DESC_LEN 51  
  
SQLCHAR *Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (?, ?, ?)";  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Prepare the INSERT statement.  
SQLPrepare(hstmt, Statement, SQL_NTS);  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Loop to continually get new values and insert them.  
while (GetNewValues(&PartID, Desc, &Price))  
   SQLExecute(hstmt);  
```  
  
 Talvez a maneira mais eficiente usar a instrução é criar um procedimento que contém a instrução, conforme mostrado no exemplo de código a seguir. Porque o procedimento é construído em tempo de desenvolvimento e armazenado na fonte de dados, ele não precisa ser preparado em tempo de execução. Uma desvantagem desse método é que a sintaxe para criação de procedimentos é específico do DBMS e procedimentos devem ser construídos separadamente para cada DBMS no qual o aplicativo será executado.  
  
```  
#define DESC_LEN 51  
  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Loop to continually get new values and insert them.  
while (GetNewValues(&PartID, Desc, &Price))  
   SQLExecDirect(hstmt, "{call InsertPart(?, ?, ?)}", SQL_NTS);  
```  
  
 Para obter mais informações sobre parâmetros, instruções preparadas e procedimentos, consulte [executando uma instrução](../../../odbc/reference/develop-app/executing-a-statement.md).
