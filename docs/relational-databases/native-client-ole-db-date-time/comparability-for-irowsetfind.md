---
title: "Comparações de IRowsetFind | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-date-time
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: IRowsetFind comparability [ODBC]
ms.assetid: 7d148b56-9bbe-4e55-b31f-43f115705402
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 89032da08d97abedcf80d250dbbd8af9fbec3fd0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="comparability-for-irowsetfind"></a>Comparações de IRowsetFind
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Somente para tipos de data/hora, IRowsetFind dá suporte às seguintes comparações:  
  
-   LT  
  
-   LE  
  
-   EQ  
  
-   GE  
  
-   GT  
  
-   NE  
  
-   IGNORE  
  
 Se for tentada qualquer outra comparação, DB_E_BADCOMPAREOP será retornado. Isso é consistente com a especificação OLE DB.  
  
## <a name="see-also"></a>Consulte Também  
 [Data e hora melhorias &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
