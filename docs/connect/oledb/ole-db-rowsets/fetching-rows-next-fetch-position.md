---
title: Próxima posição de busca | Microsoft Docs
description: Obtendo linhas - próxima posição de busca
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
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 22867097b8eb0cb89e2a1853c14d911ba2bcfab2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="fetching-rows---next-fetch-position"></a>Obtendo linhas - próxima posição de busca
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O Driver OLE DB para SQL Server mantém track da próxima posição de busca assim que uma sequência de chamadas para o **GetNextRows** método (sem ignora, as alterações de direção ou intervenção chamadas para o **FindNextRow** **Busca**, ou **RestartPosition** métodos) lê todo o conjunto de linhas sem ignorar ou repetir nenhuma linha. A próxima posição de busca é alterada chamando **GetNextRows**, **IRowset:: RestartPosition**, ou **IRowsetIndex**, ou chamando **FindNextRow** com um valor nulo *pBookmark* valor. Chamando **FindNextRow** com um nonnull *pBookmark* valor não afeta a próxima posição de busca.  
  
## <a name="see-also"></a>Consulte também  
 [Buscando linhas](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
