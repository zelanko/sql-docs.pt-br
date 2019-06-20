---
title: Atualização e persistência de dados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data [ADO]
- data updates [ADO]
- ADO, updating data
ms.assetid: 8dc27274-4f96-43d1-913c-4ff7d01b9a27
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b251da97fe14abb8b10abe974c40b9adf0b37898
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699890"
---
# <a name="updating-and-persisting-data"></a>Atualização e persistência de dados
Os capítulos anteriores discutiram como usar o ADO para acessar dados em uma fonte de dados, como mover-se nos dados e até mesmo como editar os dados. É claro que, se a meta do seu aplicativo é permitir que os usuários façam alterações aos dados, você precisará entender como salvar essas alterações. Você pode manter ou o **conjunto de registros** muda para um arquivo usando o **salvar** método, ou você pode enviar as alterações de volta para a fonte de dados para armazenamento usando o **atualização** ou  **UpdateBatch** métodos.  
  
 Nos capítulos anteriores, você alterou os dados em várias linhas do **conjunto de registros**. ADO dá suporte a dois Noções básicas relativas para a adição, exclusão e modificação de linhas de dados.  
  
 A noção de primeira é imediatamente não são feitas alterações para o **conjunto de registros**; em vez disso, elas são feitas em interno *buffer de cópia*. Se você decidir que não deseja que as alterações, as modificações no buffer de cópia serão descartadas. Se você optar por manter as alterações, as alterações no buffer de cópia são aplicadas para o **conjunto de registros**.  
  
 A noção de segundo é que as alterações são propagadas ou à fonte de dados assim que você declara o trabalho em uma linha completa (ou seja, *imediata* modo), ou todas as alterações em um conjunto de linhas são coletadas até que você declarar o trabalho para o conjunto completo (ou seja, *lote* modo). O **LockType** propriedade determina quando as alterações são feitas à fonte de dados subjacente. **adLockOptimistic** ou **adLockPessimistic** Especifica o modo imediato, enquanto **adLockBatchOptimistic** Especifica o modo de lote. O **CursorLocation** propriedade pode afetar quais **LockType** configurações estão disponíveis. Por exemplo, o **adLockPessimistic** configuração não tem suporte se o **CursorLocation** estiver definida como **adUseClient**.  
  
 No modo imediato, cada chamada a **atualização** método propaga as alterações à fonte de dados. No modo de lote, cada invocação de **atualização** ou a movimentação de posição de linha atual salva as alterações para o buffer de cópia, mas somente os **UpdateBatch** método propaga as alterações à fonte de dados.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Atualizando dados](../../../ado/guide/data/updating-data.md)  
  
-   [Persistência de dados](../../../ado/guide/data/persisting-data.md)
