---
title: SQLColumnPrivileges | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a5356d408a5116f6ab2cd6ae6e0e16d2dc7c26df
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73787479"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLColumnPrivileges** retorna SQL_SUCCESS se os valores existem ou não para os parâmetros*CatalogName*, *schemas*, *TableName*ou *ColumnName* . **SQLFetch** retorna SQL_NO_DATA quando valores inválidos são usados nesses parâmetros.  
  
 **SQLColumnPrivileges** pode ser executado em um cursor de servidor estático. Uma tentativa de executar **SQLColumnPrivileges** em um cursor atualizável (dinâmico ou de conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO indicando que o tipo de cursor foi alterado.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte ao relatório de informações de tabelas em servidores vinculados, aceitando um nome de duas partes para o parâmetro *CatalogName* : *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLColumnPrivileges](https://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
