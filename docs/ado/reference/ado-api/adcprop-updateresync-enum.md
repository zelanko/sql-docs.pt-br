---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afaadf62c38c318c759be1c452ff0953ba19c7d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065256"
---
# <a name="adcpropupdateresyncenum"></a>ADCPROP_UPDATERESYNC_ENUM
Especifica se o [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método é seguido por implícito [ressincronizar](../../../ado/reference/ado-api/resync-method.md) operação de método em caso afirmativo, o escopo da operação.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|Invoca **ressincronizar** com o valor combinado de todos os outros membros ADCPROP_UPDATERESYNC_ENUM.|  
|**adResyncAutoIncrement**|1|Padrão. Tenta recuperar o novo valor de identidade para colunas que são automaticamente incrementados ou gerados pela fonte de dados, como Microsoft Jet AutoNumber campos ou colunas de identidade do Microsoft SQL Server.|  
|**adResyncConflicts**|2|Invoca **ressincronizar** para todas as linhas em que a operação de atualização ou exclusão falhou devido a um conflito de simultaneidade.|  
|**adResyncInserts**|8|Invoca **ressincronizar** para todas as linhas inseridas com êxito. No entanto, os valores de coluna de incremento automático não são ressincronizados. Em vez disso, o conteúdo das linhas recentemente inseridas é sincronizados novamente com base no valor da chave primária existente. Se a chave primária é um valor de incremento automático **ressincronizar** não irá recuperar o conteúdo da linha pretendido. Para incrementar automaticamente valores de chave primária de incremento automático, chame **UpdateBatch** com o valor combinado **adResyncAutoIncrement** + **adResyncInserts**.|  
|**adResyncNone**|0|Não invoca **ressincronizar**.|  
|**adResyncUpdates**|4|Invoca **ressincronizar** para todas as linhas atualizadas com êxito.|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Atualizar propriedade dinâmica de ressincronização (ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
