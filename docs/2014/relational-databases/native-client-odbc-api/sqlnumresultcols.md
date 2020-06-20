---
title: SQLNumResultCols | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
author: rothja
ms.author: jroth
ms.openlocfilehash: 45e72165eef621dc377b02ed3d2e7e1e3cf7ab8e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021865"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
  Para instruções executadas, o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client não visita o servidor para informar o número de colunas em um conjunto de resultados. Nesse caso, o `SQLNumResultCols` não causa um ida e volta do servidor. Como [SQLDescribeCol](sqldescribecol.md) e [SQLColAttribute](sqlcolattribute.md), a chamada em instruções preparadas, `SQLNumResultCols` mas não executadas, gera um ida e volta do servidor.  
  
 Quando uma instrução ou lote de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] retorna vários conjuntos de linha como resultado, é possível que o número de colunas do conjunto de resultados seja alterado de um conjunto para o outro. `SQLNumResultCols`deve ser chamado para cada conjunto. Quando o número de colunas é alterado, o aplicativo deve associar novamente os valores de dados antes de buscar resultados de linha. Para obter mais informações sobre como manipular vários retornos de conjunto de resultados, consulte [SQLMoreResults](sqlmoreresults.md).  
  
 Melhorias no mecanismo de banco de dados começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir SQLNumResultCols para obter descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados pelo SQLNumResultCols em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Descoberta de metadados](../native-client/features/metadata-discovery.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLNumResultCols](https://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
