---
title: Próxima posição de busca | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
author: rothja
ms.author: jroth
ms.openlocfilehash: fcc771eef4acf603148bc4b4318e810b1bd72302
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055937"
---
# <a name="next-fetch-position"></a>Próxima posição de busca
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo controla a próxima posição de busca para que uma sequência de chamadas para o método **GetNextRows** (sem ignorar, alterações de direção ou chamadas intermediárias para os métodos **FindNextRow**, **Seek**ou **RestartPosition** ) Leia todo o conjunto de linhas sem ignorar ou repetir nenhuma linha. A próxima posição de fetch é alterada chamando **IRowset::GetNextRows**, **IRowset::RestartPosition** ou **IRowsetIndex::Seek**, ou chamando **FindNextRow** com um valor de *pBookmark* nulo. A chamada de **FindNextRow** com um valor *pBookmark* não nulo não afeta a próxima posição de fetch.  
  
## <a name="see-also"></a>Consulte Também  
 [Buscando linhas](fetching-rows.md)  
  
  
