---
description: ADCPROP_UPDATERESYNC_ENUM
title: ADCPROP_UPDATERESYNC_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords:
- ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
author: rothja
ms.author: jroth
ms.openlocfilehash: b4097bcdeb5460776017ce7a120ff43aa7a4420f
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88760240"
---
# <a name="adcprop_updateresync_enum"></a>ADCPROP_UPDATERESYNC_ENUM
Especifica se o método [UpdateBatch](./updatebatch-method.md) é seguido por uma operação de método de [ressincronização](./resync-method.md) implícita e, nesse caso, o escopo dessa operação.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|Invoca a **ressincronização** com o valor combinado de todos os outros membros ADCPROP_UPDATERESYNC_ENUM.|  
|**adResyncAutoIncrement**|1|Padrão. Tenta recuperar o novo valor de identidade para colunas que são incrementadas automaticamente ou geradas pela fonte de dados, como campos de AutoNumeração do Microsoft Jet ou Microsoft SQL Server colunas de identidade.|  
|**adResyncConflicts**|2|Invoca a **ressincronização** para todas as linhas nas quais a operação de atualização ou exclusão falhou devido a um conflito de simultaneidade.|  
|**adResyncInserts**|8|Invoca a **ressincronização** para todas as linhas inseridas com êxito. No entanto, os valores de coluna AutoIncrement não são ressincronizados. Em vez disso, o conteúdo de linhas recentemente inseridas é ressincronizado com base no valor de chave primária existente. Se a chave primária for um valor de incremento automático, a **ressincronização** não recuperará o conteúdo da linha pretendida. Para incrementar automaticamente valores de chave primária de incremento automático, chame **UpdateBatch** com o valor combinado **adResyncAutoIncrement**  +  **adResyncInserts**.|  
|**adResyncNone**|0|Não invoca a **ressincronização**.|  
|**adResyncUpdates**|4|Invoca a **ressincronização** para todas as linhas atualizadas com êxito.|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Atualizar propriedade dinâmica de ressincronização (ADO)](./update-resync-property-dynamic-ado.md)