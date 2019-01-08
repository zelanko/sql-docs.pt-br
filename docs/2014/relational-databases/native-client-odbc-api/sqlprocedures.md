---
title: SQLProcedures | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0001f1d6e45e855b884028a595a2b61263c2e58
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53365988"
---
# <a name="sqlprocedures"></a>SQLProcedures
  Todos os procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornam um valor. **SQLProcedures** reporta SQL_PT_FUNCTION para o conjunto de resultados PROCEDURE_TYPE.  
  
 **SQLProcedures** retorna SQL_SUCCESS havendo ou não valores para existir *CatalogName, SchemaName* ou *ProcName* parâmetros. **SQLFetch** retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
 **SQLProcedures** pode ser executado em um cursor de servidor estático. Uma tentativa de executar **SQLProcedures** em um cursor atualizável (dinâmico ou conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO, indicando que o tipo de cursor foi alterado.  
  
 **SQLProcedures** retorna informações sobre qualquer procedimento cujos nomes correspondam *ProcName* e pode ser executado pelo usuário atual ou para o qual o usuário atual tem permissão VIEW DEFINITION.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLProcedures](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
