---
title: Modo de lote | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 941c331c28cf5d1469b063b882bad23610a5605d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="batch-mode"></a>Modo de lote
Modo de lote está em vigor quando o **LockType** está definida como **adLockBatchOptimistic** e atualização em lotes é suportado pelo provedor. Determinadas configurações de tipo de bloqueio não estão disponíveis dependendo da posição do cursor. Por exemplo, um tipo de bloqueio pessimista não está disponível quando o **CursorLocation** é definido como **adUseClient**. Por outro lado, um provedor não oferece suporte a um bloqueio otimista de lote de quando o local do cursor está no servidor. Você deve usar o lote com um conjunto de chaves ou um cursor estático somente a atualização.  
  
 O **UpdateBatch** método é usado para enviar **registros** alterações são mantidas no buffer de cópia para o servidor para atualizar a fonte de dados. Na seção a seguir, estamos abrirá um **registros** em modo de lote, fazer alterações para o buffer de cópia e, em seguida, enviar nossas alterações para a fonte de dados usando uma chamada para **UpdateBatch**.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Enviando as atualizações: método UpdateBatch](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [Filtrando os registros atualizados](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [Lidando com atualizações de falha](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [Detectando e resolvendo conflitos](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [Desconectando e reconectando o conjunto de registros](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [Atualizando resultados JOINed: tabela única](../../../ado/guide/data/updating-joined-results-unique-table.md)
