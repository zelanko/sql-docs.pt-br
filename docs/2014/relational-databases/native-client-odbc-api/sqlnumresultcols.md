---
title: SQLNumResultCols | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c1a4825dc8d73f815f6b399c6e3a51c064d3b9b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424315"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
  Para instruções executadas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client não visita o servidor para informar o número de colunas em um conjunto de resultados. Nesse caso, `SQLNumResultCols` não causa uma ida e volta do servidor. Como o [SQLDescribeCol](sqldescribecol.md) e [SQLColAttribute](sqlcolattribute.md), chamar `SQLNumResultCols` diante preparadas, mas instruções não executadas gera uma ida e volta do servidor.  
  
 Quando uma instrução ou lote de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] retorna vários conjuntos de linha como resultado, é possível que o número de colunas do conjunto de resultados seja alterado de um conjunto para o outro. `SQLNumResultCols` deve ser chamado para cada conjunto. Quando o número de colunas é alterado, o aplicativo deve associar novamente os valores de dados antes de buscar resultados de linha. Para obter mais informações sobre como lidar com resultados múltiplos retornos de conjunto, consulte [SQLMoreResults](sqlmoreresults.md).  
  
 Melhorias no mecanismo de banco de dados a partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir SQLNumResultCols Obtenha descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados por SQLNumResultCols nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [descoberta de metadados](../native-client/features/metadata-discovery.md).  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLNumResultCols](http://go.microsoft.com/fwlink/?LinkId=59359)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
