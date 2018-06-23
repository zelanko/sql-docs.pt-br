---
title: SQLColumnPrivileges | Microsoft Docs
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
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c13c432b43be893cdc0612fe9ed54fc7b612b213
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012041"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
  **SQLColumnPrivileges** retorna SQL_SUCCESS se existirem ou não valores para o*CatalogName*, *SchemaName*, *TableName*, ou  *ColumnName* parâmetros. **SQLFetch** retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
 **SQLColumnPrivileges** pode ser executado em um cursor de servidor estático. Uma tentativa de executar **SQLColumnPrivileges** em um cursor atualizável (dinâmico ou conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO, indicando que o tipo de cursor foi alterado.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece suporte a informações de relatórios para tabelas em servidores vinculados, aceitando um nome de duas partes para o *CatalogName* parâmetro: *linked_server_name*.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLColumnPrivileges](http://go.microsoft.com/fwlink/?LinkId=59335)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  