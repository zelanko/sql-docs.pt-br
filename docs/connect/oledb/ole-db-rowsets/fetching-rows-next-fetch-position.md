---
title: Próxima posição de busca | Microsoft Docs
description: Buscando linhas – próxima posição de fetch
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 9e73572d72cb178d254c7bea1318c7fc7c68ab56
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43019883"
---
# <a name="fetching-rows---next-fetch-position"></a>Buscando linhas – próxima posição de fetch
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O OLE DB Driver for SQL Server controla a próxima posição de fetch, de forma que uma sequência de chamadas ao método **GetNextRows** (sem saltos, alterações de direção ou intervenção de chamadas aos métodos **FindNextRow**, **Seek** ou **RestartPosition**) leia todo o conjunto de linhas sem ignorar nem repetir nenhuma linha. A próxima posição de fetch é alterada chamando **IRowset::GetNextRows**, **IRowset::RestartPosition** ou **IRowsetIndex::Seek**, ou chamando **FindNextRow** com um valor de *pBookmark* nulo. A chamada de **FindNextRow** com um valor *pBookmark* não nulo não afeta a próxima posição de fetch.  
  
## <a name="see-also"></a>Consulte Também  
 [Buscando linhas](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
