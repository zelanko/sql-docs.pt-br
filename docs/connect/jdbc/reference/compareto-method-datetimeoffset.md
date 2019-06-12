---
title: Método compareTo (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e4cf2ea4-0fe9-40ce-ba79-f2a2b616997e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cb06138639be09378baa8dfe94d110c0ded41223
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66777364"
---
# <a name="compareto-method-datetimeoffset"></a>Método compareTo (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Compara essa **DateTimeOffset** objeto para outro **DateTimeOffset** objeto com base na hora de GMT.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int compareTo(DateTimeOffset other)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Um valor [DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) que você deseja comparar com a instância atual.  
  
## <a name="return-value"></a>Valor retornado  
 A tabela a seguir descreve o valor de retorno do método:  
  
|Valor retornado|Descrição|  
|------------------|-----------------|  
|0|Ambos **DateTimeOffset** objetos representam o mesmo ponto no tempo.|  
|número negativo|Isso **DateTimeOffset** objeto representa um ponto no tempo anterior *outros*.|  
|número positivo|Isso **DateTimeOffset** objeto representa um ponto no tempo que está depois *outros*.|  
  
## <a name="remarks"></a>Remarks  
 Quando dois objetos **DateTimeOffset** tiverem a mesma hora em GMT, não haverá nenhuma organização adicional dos objetos com base no deslocamento.  
  
## <a name="see-also"></a>Consulte Também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
