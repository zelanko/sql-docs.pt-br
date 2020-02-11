---
title: SQLSpecialColumns | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSpecialColumns function
ms.assetid: dffe02ed-8f79-4c9a-af34-98130bbe5462
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ea811151e9c81ed515b774f279297d236c608f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63188734"
---
# <a name="sqlspecialcolumns"></a>SQLSpecialColumns
  Ao pedir identificadores de linha (*IdentifierType* SQL_BEST_ROWID), **SQLSpecialColumns** retorna um conjunto de resultados vazio (nenhuma linha de dados) para qualquer escopo solicitado que não seja SQL_SCOPE_CURROW. O conjunto de resultados gerado indica que as colunas são válidas somente dentro desse escopo.  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte a pseudocolunas para identificadores. O conjunto de resultados de **SQLSpecialColumns** identificará todas as colunas como SQL_PC_NOT_PSEUDO.  
  
 **SQLSpecialColumns** pode ser executado em um cursor estático. Uma tentativa de executar **SQLSpecialColumns** em um cursor atualizável (controlado por conjunto de chaves ou dinâmico) retorna SQL_SUCCESS_WITH_INFO, indicando que indica o tipo de cursor foi alterado.  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>Suporte de SQLSpecialColumns a recursos aprimorados de data e hora  
 Para obter informações sobre os valores de retorno para as colunas DATA_TYPE, TYPE_NAME, COLUMN_SIZE, BUFFER_LENGTH e DECIMAL_DIGTS para tipos de data/hora, consulte [Catalog Metadata](../native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obter mais informações gerais, consulte [melhorias de data e hora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>Suporte a SQLSpecialColumns para UDTs grandes do CLR  
 O **SQLSpecialColumns** dá suporte a UDTs (tipos definidos pelo usuário) CLR grandes. Para obter mais informações, consulte [tipos CLR grandes definidos pelo usuário &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLSpecialColumns](https://go.microsoft.com/fwlink/?LinkId=59371)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
