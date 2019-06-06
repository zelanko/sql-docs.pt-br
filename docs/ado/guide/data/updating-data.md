---
title: Atualização de dados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], about data updates
- updating data [ADO], about updating data
ms.assetid: 6508e4e9-e33a-4dad-b340-5d632fd78a91
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8ea95b7d34f1395f6322d9a6ad6a0229bb8c7e45
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704571"
---
# <a name="updating-data"></a>Atualizando dados
Comportamento de atualização e a funcionalidade depende praticamente atualizar modo (tipo de bloqueio), o tipo de cursor e o local do cursor.  
  
 Use o **atualização** método para salvar quaisquer alterações feitas no registro atual de uma **conjunto de registros** objeto desde a chamada a **AddNew** método ou desde que alterar quaisquer valores de campo em um registro existente. O **Recordset** objeto deve dar suporte a atualizações.  
  
 Se o **conjunto de registros** objeto dá suporte à atualização em lotes, você pode armazenar em cache várias alterações para um ou mais registros localmente até que você chame a **UpdateBatch** método. Se você estiver editando o registro atual ou adicionar um novo registro, quando você chama o **UpdateBatch** método, ADO chamará automaticamente a **atualização** método para salvar todas as alterações pendentes no registro atual antes de transmitir as alterações em lote para o provedor.  
  
 O registro atual permanece atual depois de chamar o **atualização** ou **UpdateBatch** métodos.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Modo imediato](../../../ado/guide/data/immediate-mode.md)  
  
-   [Modo de lote](../../../ado/guide/data/batch-mode.md)  
  
-   [Processamento de transações](../../../ado/guide/data/transaction-processing.md)
