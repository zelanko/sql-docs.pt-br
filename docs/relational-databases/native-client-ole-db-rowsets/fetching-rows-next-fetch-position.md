---
title: "Próxima posição de busca | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 838e550243b54fc6392ece40a42ff0bdd3fc0d91
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="fetching-rows---next-fetch-position"></a>Obtendo linhas - próxima posição de busca
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider mantém o controle da próxima posição de busca assim que uma sequência de chamadas para o **GetNextRows** método (sem ignora, as alterações de direção ou intervenção chamadas para o  **FindNextRow**, **busca**, ou **RestartPosition** métodos) lê todo o conjunto de linhas sem ignorar ou repetir nenhuma linha. A próxima posição de busca é alterada chamando **GetNextRows**, **IRowset:: RestartPosition**, ou **IRowsetIndex**, ou chamando **FindNextRow** com um valor nulo *pBookmark* valor. Chamando **FindNextRow** com um nonnull *pBookmark* valor não afeta a próxima posição de busca.  
  
## <a name="see-also"></a>Consulte Também  
 [Buscando linhas](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
  
