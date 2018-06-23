---
title: SQLPrimaryKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cb0dc440025730c278206a751a5ce741b69b0f6e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008414"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
  Uma tabela pode ter uma coluna ou colunas que podem servir como identificadores de linha exclusivo e tabelas criadas sem uma restrição PRIMARY KEY retornam um resultado vazio definido como SQLPrimaryKeys. A função ODBC [SQLSpecialColumns](sqlspecialcolumns.md) candidatos de identificador para tabelas sem chaves primárias de linhas de relatórios.  
  
 SQLPrimaryKeys retorna SQL_SUCCESS se existirem ou não valores para *CatalogName*, *SchemaName*, ou *TableName* parâmetros. SQLFetch retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
 SQLPrimaryKeys pode ser executado em um cursor de servidor estático. Uma tentativa de executar SQLPrimaryKeys em um cursor atualizável (dinâmico ou conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO, indicando que o tipo de cursor foi alterado.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece suporte a informações de relatórios para tabelas em servidores vinculados, aceitando um nome de duas partes para o *CatalogName* parâmetro: *linked_server_name*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys e parâmetros com valor de tabela  
 Se o atributo de instrução SQL_SOPT_SS_NAME_SCOPE tiver o valor SQL_SS_NAME_SCOPE_TABLE_TYPE, em vez de seu valor padrão sql_ss_name_scope_table, SQLPrimaryKeys retornará informações sobre colunas de chave primária de tipos de tabela. Para obter mais informações sobre SQL_SOPT_SS_NAME_SCOPE, consulte [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLPrimaryKeys](http://go.microsoft.com/fwlink/?LinkId=59361)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  