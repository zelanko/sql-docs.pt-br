---
description: Modo de lote
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
ms.openlocfilehash: 353e5ae0fe15fb21f04f6efcc97195a5e237b58e
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806401"
---
# <a name="batch-mode"></a>Modo de lote
O modo de lote está em vigor quando a propriedade **LockType** está definida como **adLockBatchOptimistic** e a atualização do lote é suportada pelo provedor. Determinadas configurações de tipo de bloqueio não estão disponíveis dependendo do local do cursor. Por exemplo, um tipo de bloqueio pessimista não está disponível quando **CursorLocation** é definido como **adUseClient**. Por outro lado, um provedor não pode dar suporte a um bloqueio otimista em lote quando o local do cursor está no servidor. Você deve usar a atualização em lotes somente com um conjunto de chaves ou cursor estático.  
  
 O método **UpdateBatch** é usado para enviar alterações de **conjunto de registros** mantidas no buffer de cópia para o servidor para atualizar a fonte de dados. Na seção a seguir, vamos abrir um **conjunto de registros** no modo de lote, fazer alterações no buffer de cópia e enviar nossas alterações para a fonte de dados usando uma chamada para **UpdateBatch**.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Enviar as atualizações: método UpdateBatch](./sending-the-updates-updatebatch-method.md)  
  
-   [Filtrar os registros atualizados](./filtering-for-updated-records.md)  
  
-   [Lidar com atualizações de falha](./dealing-with-failed-updates.md)  
  
-   [Detectando e solucionando conflitos](./detecting-and-resolving-conflicts.md)  
  
-   [Desconectar e reconectar o conjunto de registros](./disconnecting-and-reconnecting-the-recordset.md)  
  
-   [Atualizar resultados JOINed: tabela única](./updating-joined-results-unique-table.md)