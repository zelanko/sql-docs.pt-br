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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 188a95f985ac1d578bca8c7e10ac4c4054c935c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925950"
---
# <a name="batch-mode"></a>Modo de lote
O modo de lote está em vigor quando a propriedade **LockType** está definida como **adLockBatchOptimistic** e a atualização do lote é suportada pelo provedor. Determinadas configurações de tipo de bloqueio não estão disponíveis dependendo do local do cursor. Por exemplo, um tipo de bloqueio pessimista não está disponível quando **CursorLocation** é definido como **adUseClient**. Por outro lado, um provedor não pode dar suporte a um bloqueio otimista em lote quando o local do cursor está no servidor. Você deve usar a atualização em lotes somente com um conjunto de chaves ou cursor estático.  
  
 O método **UpdateBatch** é usado para enviar alterações de **conjunto de registros** mantidas no buffer de cópia para o servidor para atualizar a fonte de dados. Na seção a seguir, vamos abrir um **conjunto de registros** no modo de lote, fazer alterações no buffer de cópia e enviar nossas alterações para a fonte de dados usando uma chamada para **UpdateBatch**.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Enviar as atualizações: método UpdateBatch](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [Filtrar os registros atualizados](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [Lidar com atualizações de falha](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [Detectando e solucionando conflitos](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [Desconectar e reconectar o conjunto de registros](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [Atualizar resultados JOINed: tabela única](../../../ado/guide/data/updating-joined-results-unique-table.md)
