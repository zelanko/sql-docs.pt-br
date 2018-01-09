---
title: SQLSpecialColumns | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLSpecialColumns function
ms.assetid: dffe02ed-8f79-4c9a-af34-98130bbe5462
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3811adfc521b4f179776bea8660fe33df5900246
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="sqlspecialcolumns"></a>SQLSpecialColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Ao pedir identificadores de linha (*IdentifierType* SQL_BEST_ROWID), **SQLSpecialColumns** retorna um conjunto de resultados vazio (nenhuma linha de dados) para qualquer escopo solicitado que não seja SQL_SCOPE_CURROW. O conjunto de resultados gerado indica que as colunas são válidas somente dentro desse escopo.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte a pseudocolunas para identificadores. O conjunto de resultados de **SQLSpecialColumns** identificará todas as colunas como SQL_PC_NOT_PSEUDO.  
  
 É possível executar**SQLSpecialColumns** em um cursor estático. Uma tentativa de executar **SQLSpecialColumns** em um cursor atualizável (controlado por conjunto de chaves ou dinâmico) retorna SQL_SUCCESS_WITH_INFO, indicando que indica o tipo de cursor foi alterado.  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>Suporte de SQLSpecialColumns a recursos aprimorados de data e hora  
 Para obter informações sobre os valores retornados para as colunas DATA_TYPE, TYPE_NAME, COLUMN_SIZE, BUFFER_LENGTH e DECIMAL_DIGTS para tipos de data/hora, consulte [metadados de catálogo](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obter mais informações, consulte [data e hora melhorias &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>Suporte a SQLSpecialColumns para UDTs grandes do CLR  
 **SQLSpecialColumns** dá suporte a UDTs grandes do CLR. Para obter mais informações, consulte [Large CLR User-Defined tipos &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLSpecialColumns](http://go.microsoft.com/fwlink/?LinkId=59371)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
