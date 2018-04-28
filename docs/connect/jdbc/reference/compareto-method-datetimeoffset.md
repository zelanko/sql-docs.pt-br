---
title: Método compareTo (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e4cf2ea4-0fe9-40ce-ba79-f2a2b616997e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b8307787576f520f83ceeffe10c830cd06a16d69
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="compareto-method-datetimeoffset"></a>Método compareTo (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Compara este **DateTimeOffset** objeto para outro **DateTimeOffset** objeto com base na hora GMT.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int compareTo(DateTimeOffset other)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Um [DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) valor que você deseja comparar com a instância atual.  
  
## <a name="return-value"></a>Valor de retorno  
 A tabela a seguir descreve o valor de retorno do método:  
  
|Valor retornado|Description|  
|------------------|-----------------|  
|0|Ambos **DateTimeOffset** objetos representam o mesmo ponto no tempo.|  
|número negativo|Isso **DateTimeOffset** objeto representa um ponto no tempo anterior *outros*.|  
|número positivo|Isso **DateTimeOffset** objeto representa um ponto no tempo após *outros*.|  
  
## <a name="remarks"></a>Remarks  
 Quando dois **DateTimeOffset** objetos com a mesma hora GMT, não há nenhuma organização adicional dos objetos com base no deslocamento.  
  
## <a name="see-also"></a>Consulte também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
