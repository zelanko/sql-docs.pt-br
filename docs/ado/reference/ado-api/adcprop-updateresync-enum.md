---
title: ADCPROP_UPDATERESYNC_ENUM | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords:
- ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e5c25ab6802b6a99902c9e52990be80ff14ed6d5
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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

