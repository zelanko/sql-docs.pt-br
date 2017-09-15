---
title: "Atualização e persistir dados | Microsoft Docs"
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
- updating data [ADO]
- data updates [ADO]
- ADO, updating data
ms.assetid: 8dc27274-4f96-43d1-913c-4ff7d01b9a27
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c08f7bfbb813bb3e2041f350a2e4397d9aff6ffd
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="updating-and-persisting-data"></a>Atualizar e manter dados
Os capítulos anteriores discutimos como usar o ADO para acessar dados em uma fonte de dados, como mover-se nos dados e até mesmo como editar os dados. É claro que, se for o objetivo do seu aplicativo permitir que os usuários façam alterações aos dados, você precisará entender como salvar as alterações. Ou você pode persistir o **registros** muda para um arquivo usando o **salvar** método, ou você pode enviar as alterações de volta para a fonte de dados para armazenamento usando o **atualização** ou ** UpdateBatch** métodos.  
  
 Nos capítulos anteriores, você alterou os dados em várias linhas do **registros**. ADO dá suporte a dois Noções básicas relacionadas para a adição, exclusão e modificação de linhas de dados.  
  
 A noção de primeira é que as alterações não são feitas imediatamente para o **registros**; em vez disso, são feitas interno *buffer de cópia*. Se você decidir que não deseja que as alterações, as modificações no buffer de cópia são descartadas. Se você optar por manter as alterações, as alterações no buffer de cópia são aplicadas para o **registros**.  
  
 A noção de segundo é que as alterações são propagadas ou à fonte de dados assim que você declarar o trabalho em uma linha completa (ou seja, *imediata* modo), ou todas as alterações em um conjunto de linhas são coletadas até que você declarar o trabalho para o conjunto completo (ou seja, *lote* modo). O **LockType** propriedade determina quando as alterações são feitas à fonte de dados subjacente. **adLockOptimistic** ou **adLockPessimistic** Especifica o modo imediato, enquanto **adLockBatchOptimistic** Especifica o modo de lote. O **CursorLocation** propriedade pode afetar que **LockType** configurações estão disponíveis. Por exemplo, o **adLockPessimistic** configuração não é suportada se o **CursorLocation** está definida como **adUseClient**.  
  
 No modo imediato, cada chamada a **atualização** método propaga as alterações para a fonte de dados. No modo de lote, cada invocação do **atualização** ou movimentação da posição atual da linha salva as alterações para o buffer de cópia, mas apenas o **UpdateBatch** método propaga as alterações para a fonte de dados.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Atualizando dados](../../../ado/guide/data/updating-data.md)  
  
-   [Persistência de dados](../../../ado/guide/data/persisting-data.md)
