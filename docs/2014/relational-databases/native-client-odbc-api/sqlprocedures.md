---
title: SQLProcedures | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a7855016bf7c0dec86775cc6a1a289d0b317031
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417715"
---
# <a name="sqlprocedures"></a>SQLProcedures
  Todos os procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornam um valor. **SQLProcedures** reporta SQL_PT_FUNCTION para o conjunto de resultados PROCEDURE_TYPE.  
  
 **SQLProcedures** retorna SQL_SUCCESS havendo ou não valores para existir *CatalogName, SchemaName* ou *ProcName* parâmetros. **SQLFetch** retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
 **SQLProcedures** pode ser executado em um cursor de servidor estático. Uma tentativa de executar **SQLProcedures** em um cursor atualizável (dinâmico ou conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO, indicando que o tipo de cursor foi alterado.  
  
 **SQLProcedures** retorna informações sobre qualquer procedimento cujos nomes correspondam *ProcName* e pode ser executado pelo usuário atual ou para o qual o usuário atual tem permissão VIEW DEFINITION.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLProcedures](http://go.microsoft.com/fwlink/?LinkId=59364)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
