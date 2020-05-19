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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a6208467b4d6af6b0417727643e190b8702968ea
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702130"
---
# <a name="sqlspecialcolumns"></a>SQLSpecialColumns
  Ao pedir identificadores de linha (*IdentifierType* SQL_BEST_ROWID), **SQLSpecialColumns** retorna um conjunto de resultados vazio (nenhuma linha de dados) para qualquer escopo solicitado que não seja SQL_SCOPE_CURROW. O conjunto de resultados gerado indica que as colunas são válidas somente dentro desse escopo.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte a pseudocolunas para identificadores. O conjunto de resultados de **SQLSpecialColumns** identificará todas as colunas como SQL_PC_NOT_PSEUDO.  
  
 É possível executar**SQLSpecialColumns** em um cursor estático. Uma tentativa de executar **SQLSpecialColumns** em um cursor atualizável (controlado por conjunto de chaves ou dinâmico) retorna SQL_SUCCESS_WITH_INFO, indicando que indica o tipo de cursor foi alterado.  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>Suporte de SQLSpecialColumns a recursos aprimorados de data e hora  
 Para obter informações sobre os valores de retorno para as colunas DATA_TYPE, TYPE_NAME, COLUMN_SIZE, BUFFER_LENGTH e DECIMAL_DIGTS para tipos de data/hora, consulte [Catalog Metadata](../native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obter mais informações gerais, consulte [melhorias de data e hora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>Suporte a SQLSpecialColumns para UDTs grandes do CLR  
 **SQLSpecialColumns** dá suporte a UDTs grandes do CLR. Para obter mais informações, consulte [tipos CLR grandes definidos pelo usuário &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLSpecialColumns](https://go.microsoft.com/fwlink/?LinkId=59371)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
