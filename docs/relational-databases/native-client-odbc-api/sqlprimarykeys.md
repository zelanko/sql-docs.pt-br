---
title: SQLPrimaryKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 63b1ce32a3e2be765666e0d12ceeb4d9ce290d01
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85788005"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Uma tabela pode ter uma coluna ou colunas que podem servir como identificadores de linha exclusivos, e tabelas criadas sem uma restrição de chave primária retornam um conjunto de resultados vazio para SQLPrimaryKeys. A função ODBC [SQLSpecialColumns](../../relational-databases/native-client-odbc-api/sqlspecialcolumns.md) relata candidatos de identificador de linha para tabelas sem chaves primárias.  
  
 SQLPrimaryKeys retorna SQL_SUCCESS se os valores existem ou não para os parâmetros *CatalogName*, *schemas*ou *TableName* . SQLFetch retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
 SQLPrimaryKeys pode ser executado em um cursor de servidor estático. Uma tentativa de executar SQLPrimaryKeys em um cursor atualizável (dinâmico ou de conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO indicando que o tipo de cursor foi alterado.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte ao relatório de informações de tabelas em servidores vinculados, aceitando um nome de duas partes para o parâmetro *CatalogName* : *Linked_Server_Name.Catalog_Name*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys e parâmetros com valor de tabela  
 Se o atributo de instrução SQL_SOPT_SS_NAME_SCOPE tiver o valor SQL_SS_NAME_SCOPE_TABLE_TYPE, em vez de seu valor padrão de SQL_SS_NAME_SCOPE_TABLE, SQLPrimaryKeys retornará informações sobre as colunas de chave primária dos tipos de tabela. Para obter mais informações sobre SQL_SOPT_SS_NAME_SCOPE, consulte [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLPrimaryKeys](https://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
