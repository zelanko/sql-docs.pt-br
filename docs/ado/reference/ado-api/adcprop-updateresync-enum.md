---
title: ADCPROP_UPDATERESYNC_ENUM | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords: ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d030fa1643cbf836a7380dd3113236ec7961b8d0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="adcpropupdateresyncenum"></a>ADCPROP_UPDATERESYNC_ENUM
Especifica se o [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método é seguido por um implícita [Resync](../../../ado/reference/ado-api/resync-method.md) operação de método e nesse caso, o escopo dessa operação.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|Invoca **Resync** com o valor combinado de todos os outros membros ADCPROP_UPDATERESYNC_ENUM.|  
|**adResyncAutoIncrement**|1|Padrão. Tenta recuperar o novo valor de identidade para colunas que são automaticamente incrementados ou gerados pela fonte de dados, como campos de numeração automática do Microsoft Jet ou colunas de identidade do Microsoft SQL Server.|  
|**adResyncConflicts**|2|Invoca **Resync** para todas as linhas em que a operação de atualização ou exclusão falhou devido a um conflito de simultaneidade.|  
|**adResyncInserts**|8|Invoca **Resync** para todas as linhas inseridas com êxito. No entanto, os valores de coluna de incremento automático não sincronizados novamente. Em vez disso, o conteúdo das linhas recentemente inseridas é sincronizados novamente com base no valor da chave primária existente. Se a chave primária é um valor de incremento automático, **Resync** não recuperar o conteúdo da linha pretendido. Para incrementar automaticamente valores de chave primária de incremento automático, chame **UpdateBatch** com o valor combinado **adResyncAutoIncrement** + **adResyncInserts**.|  
|**adResyncNone**|0|Não chama **Resync**.|  
|**adResyncUpdates**|4|Invoca **Resync** para todas as linhas atualizadas com êxito.|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Atualizar propriedade dinâmica de ressincronização (ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
