---
title: Hiperprocedimentos | Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1a0464cd8a91db43f9629bed3cc9e45e48a8f7c3
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705907"
---
# <a name="sqlprocedures"></a>SQLProcedures
  Todos os procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornam um valor. A SQL_PT_FUNCTION de relatórios **SQLProcedures** para a coluna do conjunto de resultados PROCEDURE_TYPE.  
  
 **SQLProcedures** retorna SQL_SUCCESS se os valores existem ou não para os parâmetros *CatalogName, schemas* ou *ProcName* . **SQLFetch** retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
 **SQLProcedures** pode ser executado em um cursor de servidor estático. Uma tentativa de executar **Hiperprocedimentos** em um cursor atualizável (dinâmico ou de conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO, indicando que o tipo de cursor foi alterado.  
  
 **SQLProcedures** retorna informações sobre os procedimentos cujos nomes correspondem a *ProcName* e podem ser executados pelo usuário atual ou para os quais o usuário atual recebeu a permissão VIEW DEFINITION.  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLProcedures](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
