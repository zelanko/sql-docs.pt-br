---
title: Modo de lote | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 92e249a7c2d5b0c01e291f4829d5c4f8c580fb2c
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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
