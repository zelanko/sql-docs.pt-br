---
title: Próxima posição de busca | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 59af82cea07c73f346c4c8add2cd73e3de2444cc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009124"
---
# <a name="next-fetch-position"></a>Próxima posição de busca
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider mantém o controle da próxima posição de busca assim que uma sequência de chamadas para o **GetNextRows** método (sem ignora, as alterações de direção ou intervenção chamadas para o  **FindNextRow**, **busca**, ou **RestartPosition** métodos) lê todo o conjunto de linhas sem ignorar ou repetir nenhuma linha. A próxima posição de busca é alterada chamando **GetNextRows**, **IRowset:: RestartPosition**, ou **IRowsetIndex**, ou chamando **FindNextRow** com um valor nulo *pBookmark* valor. Chamando **FindNextRow** com um nonnull *pBookmark* valor não afeta a próxima posição de busca.  
  
## <a name="see-also"></a>Consulte também  
 [Buscando linhas](fetching-rows.md)  
  
  