---
description: ADCPROP_UPDATERESYNC_ENUM
title: ADCPROP_UPDATERESYNC_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 2fcf60974612325e8af7501eaa6066d96d9f2985
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976817"
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