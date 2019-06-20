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
manager: jroth
ms.openlocfilehash: 39130be0e6be31700f70002726f3aaf674aa4c82
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700923"
---
# <a name="batch-mode"></a>Modo de lote
Modo de lote está em vigor quando o **LockType** estiver definida como **adLockBatchOptimistic** e atualização em lote é suportado pelo provedor. Determinadas configurações de tipo de bloqueio não estão disponíveis dependendo do local do cursor. Por exemplo, um tipo de bloqueio pessimista não está disponível quando o **CursorLocation** é definido como **adUseClient**. Por outro lado, um provedor não oferece suporte a um bloqueio otimista de lote de quando o local do cursor está no servidor. Você deve usar o lote de atualização com um conjunto de chaves ou apenas o cursor estático.  
  
 O **UpdateBatch** método é usado para enviar **Recordset** as alterações são mantidas no buffer de cópia para o servidor para atualizar a fonte de dados. Na seção a seguir, podemos abrirá uma **conjunto de registros** no modo de lote, fazer alterações para o buffer de cópia e, em seguida, enviar nossas alterações à fonte de dados usando uma chamada para **UpdateBatch**.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Enviar as atualizações: Método UpdateBatch](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [Filtrando os registros atualizados](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [Lidando com atualizações de falha](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [Detectando e resolvendo conflitos](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [Desconectando e reconectando o conjunto de registros](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [Atualizando resultados JOINed: Tabela exclusiva](../../../ado/guide/data/updating-joined-results-unique-table.md)
