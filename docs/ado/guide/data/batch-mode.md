---
title: Modo de lote | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
author: rothja
ms.author: jroth
ms.openlocfilehash: b7e4ce2e8928ac7b4225ae58b25c6610c64832f7
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761242"
---
# <a name="batch-mode"></a>Modo de lote
O modo de lote está em vigor quando a propriedade **LockType** está definida como **adLockBatchOptimistic** e a atualização do lote é suportada pelo provedor. Determinadas configurações de tipo de bloqueio não estão disponíveis dependendo do local do cursor. Por exemplo, um tipo de bloqueio pessimista não está disponível quando **CursorLocation** é definido como **adUseClient**. Por outro lado, um provedor não pode dar suporte a um bloqueio otimista em lote quando o local do cursor está no servidor. Você deve usar a atualização em lotes somente com um conjunto de chaves ou cursor estático.  
  
 O método **UpdateBatch** é usado para enviar alterações de **conjunto de registros** mantidas no buffer de cópia para o servidor para atualizar a fonte de dados. Na seção a seguir, vamos abrir um **conjunto de registros** no modo de lote, fazer alterações no buffer de cópia e enviar nossas alterações para a fonte de dados usando uma chamada para **UpdateBatch**.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Enviar as atualizações: método UpdateBatch](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [Filtrar os registros atualizados](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [Lidando com atualizações de falha](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [Detectando e solucionando conflitos](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [Desconectando e reconectando o conjunto de registros](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [Atualizar resultados JOINed: tabela única](../../../ado/guide/data/updating-joined-results-unique-table.md)
