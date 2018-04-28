---
title: Ressincronizando linhas | Microsoft Docs
description: Ressincronizando linhas usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9dd0506deccd11250ed5251a18fe074325920b30
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>Atualizando dados em conjuntos de linhas - ressincronizando linhas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O Driver OLE DB para SQL Server dá suporte a **IRowsetResynch** em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com suporte de cursor apenas conjuntos de linhas. **IRowsetResynch** não está disponível sob demanda. O consumidor deve solicitar a interface antes de abrir o conjunto de linhas.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizando dados em conjuntos de linhas](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
