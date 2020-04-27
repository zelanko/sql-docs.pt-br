---
title: SQLTables | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLTables function
ms.assetid: 77b6c15c-9cf7-4019-b3f0-3d27d23ef656
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8209bf586e5a0b288b4975869ee8903a73a27f06
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63188669"
---
# <a name="sqltables"></a>SQLTables
  SQLTables pode ser executado em um cursor de servidor estático. Uma tentativa de executar SQLTables em um cursor atualizável (dinâmico ou de conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO indicando que o tipo de cursor foi alterado.  
  
 SQLTables relata tabelas de todos os bancos de dados quando o parâmetro *CatalogName* é SQL_ALL_CATALOGS e todos os outros parâmetros contêm valores padrão (PONTEIROs nulos).  
  
 Para relatar os catálogos, os esquemas e os tipos de tabela disponíveis, o SQLTables faz uso especial de cadeias de caracteres vazias (ponteiros de byte de comprimento zero). As cadeias de caracteres vazias não são os valores padrões (ponteiros NULL).  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte ao relatório de informações de tabelas em servidores vinculados, aceitando um nome de duas partes para o parâmetro *CatalogName* : *Linked_Server_Name.Catalog_Name*.  
  
 SQLTables retorna informações sobre todas as tabelas cujos nomes correspondem a *TableName* e pertencem ao usuário atual.  
  
## <a name="sqltables-and-table-valued-parameters"></a>SQLTables e parâmetros com valor de tabela  
 Quando o atributo de instrução SQL_SOPT_SS_NAME_SCOPE tem o valor SQL_SS_NAME_SCOPE_TABLE_TYPE, em vez de seu valor padrão de SQL_SS_NAME_SCOPE_TABLE, SQLTables retorna informações sobre tipos de tabela. O valor de TABLE_TYPE retornado para um tipo de tabela na coluna 4 do conjunto de resultados retornado por SQLTables é o tipo de tabela. Para obter mais informações sobre SQL_SOPT_SS_NAME_SCOPE, consulte [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 Tabelas, exibições e sinônimos compartilham um namespace comum que é diferente do namespace usado por tipos de tabela. Apesar de não ser possível ter uma tabela e uma exibição com o mesmo nome, é possível ter uma tabela de um tipo de tabela com o mesmo nome, no mesmo catálogo e no mesmo esquema.  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="example"></a>Exemplo  
  
```  
// Get a list of all tables in the current database.  
SQLTables(hstmt, NULL, 0, NULL, 0, NULL, 0, NULL,0);  
  
// Get a list of all tables in all databases.  
SQLTables(hstmt, (SQLCHAR*) "%", SQL_NTS, NULL, 0, NULL, 0, NULL,0);  
  
// Get a list of databases on the current connection's server.  
SQLTables(hstmt, (SQLCHAR*) "%", SQL_NTS, (SQLCHAR*)"", 0, (SQLCHAR*)"",  
    0, NULL, 0);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLTables](https://go.microsoft.com/fwlink/?LinkId=59374)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
