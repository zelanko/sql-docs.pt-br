---
title: Próxima posição de busca | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 736588819ff749623f5a12629cbd4d9844fdaacf
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43110273"
---
# <a name="fetching-rows---next-fetch-position"></a>Buscar linhas – próxima posição de fetch
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider controla a próxima posição de busca até que uma sequência de chamadas para o **GetNextRows** método (sem ignora, alterações de direção ou intervenção chamadas para o  **FindNextRow**, **busca**, ou **RestartPosition** métodos) lê todo o conjunto de linhas sem ignorar ou repetir nenhuma linha. A próxima posição de fetch é alterada chamando **IRowset::GetNextRows**, **IRowset::RestartPosition** ou **IRowsetIndex::Seek**, ou chamando **FindNextRow** com um valor de *pBookmark* nulo. A chamada de **FindNextRow** com um valor *pBookmark* não nulo não afeta a próxima posição de fetch.  
  
## <a name="see-also"></a>Consulte também  
 [Buscando linhas](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
  
