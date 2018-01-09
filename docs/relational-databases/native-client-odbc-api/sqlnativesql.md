---
title: SQLNativeSql | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
helpviewer_keywords: SQLNativeSql function
ms.assetid: 2d999fec-9e22-4514-ad5f-22a64b82f95b
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 88253aeb8af1193022eae94f49a8c93d8b7f5f8e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="sqlnativesql"></a>SQLNativeSql
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client atende a solicitações de **SQLNativeSql** sem visitar o servidor. A função testa a sintaxe de instruções SQL de forma eficaz. A verificação de sintaxe não determina se os identificadores ou os resultados de expressões nas instruções SQL são válidos e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native SQL retornado pela função **SQLNativeSql** pode apresentar falha na execução.  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLNativeSql](http://go.microsoft.com/fwlink/?LinkID=59358)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
