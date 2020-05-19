---
title: SQLColumnPrivileges | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 35bd61c12933dac25ac90d8b56afb0e17b44d3ab
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706330"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
  **SQLColumnPrivileges** retorna SQL_SUCCESS se os valores existem ou não para os parâmetros*CatalogName*, *schemas*, *TableName*ou *ColumnName* . **SQLFetch** retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
 **SQLColumnPrivileges** pode ser executado em um cursor de servidor estático. Uma tentativa de executar **SQLColumnPrivileges** em um cursor atualizável (dinâmico ou de conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO indicando que o tipo de cursor foi alterado.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte ao relatório de informações de tabelas em servidores vinculados, aceitando um nome de duas partes para o parâmetro *CatalogName* : *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLColumnPrivileges](https://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
